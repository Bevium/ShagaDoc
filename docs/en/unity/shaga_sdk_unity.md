## ShagaSDK for Unity

This section is going to show the use of the `ShagaSDK for Unity` written in `C#`.

#### Integration steps
1. Add `ShagaSDK` library reference to our project
2. Interact with the SDK through the `static class ShagaSDK`

### `ShagaSDK static class`
___
>Its scope is to send/receive some specific well defined `Messages` listed above:
>1. `AuthMessage`
>2. `DRMMessage`
>3. `CreateAndSendTransactionRequest`
>   - Brings a list of `TransactionInstruction`
>4. `MintMessage`
>5`TransactionSignMessage`
>6`AchievementMessage`
___
#### 1. `AuthMessage`
Authentication process is transparent for the user and starts when a `Wallet` is connected through the `dApp FrontEnd`.

If `ShagaServerSDK` verifies the `public key` of the user which signs the challenge trough the `Wallet`, the user will be authenticated and its `public key` will be sent to the `ShagaSDK` through the `ws:3101` previously opened.

From now on each `ShagaSDK` request will contain the `public key` of the authenticated user.

#### 2. `DRMMessage`
Digital Rights Management check is also performed automatically by the `SDK` itself right after the authentication phase.

If the verification fails, the `ShagaSDK` will not authorize any request.
#### 3. `CreateAndSendTransactionRequest` for the `SystemProgram.transfer`
<details><summary>Example Code Snippet</summary>

```csharp
void ExampleFunction() {
    TransferParams TransferParams = new TransferParams
    {
        Lamports = 12,
        ToPubKey = new PublicKey("well-formed-public-key"),
        FromPubKey = new PublicKey("well-formed-public-key")
    };
    
    TransactionInstruction TransferInstruction = new TransactionInstruction
	{
		Type = "SystemProgram.transfer",
		Params = TransferParams
	};
    
    List<TransactionInstruction> InstructionsList = new List<TransactionInstruction>();
    InstructionsList.Add(TransferInstruction);
    
    CreateAndSendTransactionRequest Req = new CreateAndSendTransactionRequest
    {
        TransactionInstructionsList = InstructionsList,
        PublicKey = new PublicKey("my-well-formed-public-key")
    }
    
    // Use the provided EventHandler to hook the Task completion
    ShagaSDK.RequestSent += OnRequestSent;
    
    try
    {
        ShagaSDK.SendTransactionInstructionsRequest(req);
    }
    catch (Exception e)
    {
        Logger.Log(Logger.LogLevel.Error, Logger.GetActualMethodName(), e.GetType().Name, e.Message);
    }
}


void OnRequestSent(object? sender, RequestArgs<BaseMessage> requestArgs)
{
    // here you can invoke the right handler switching on the requestArgs.Request.GetType()...
}
}
```
</details>