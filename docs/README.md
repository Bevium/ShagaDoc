#### SDK Documentation
# Shaga Environment SDK

The `Shaga SDK` aims to provide developers with the ability to interact with the Shaga environment directly from their games built in Unreal Engine and Unity.

By leveraging this SDK, developers can enhance their games with the Solana web3 environment interaction.

[//]: # (### Features)

[//]: # (**Cross-Platform Compatibility**: The SDK supports game development in Unreal Engine, &#40;Unity, and Godot?&#41;, ensuring compatibility across multiple platforms.)

[//]: # ()
[//]: # (**Real-Time Interaction**: With the Shaga Environment SDK, developers can create real-time interactions within their games, allowing players to engage with the environment in meaningful ways.)

[//]: # ()
[//]: # (**Seamless Integration**: Integrating the SDK into your game is straightforward, thanks to comprehensive documentation, sample code snippets, and dedicated developer support.)

[//]: # ()
[//]: # (**Scalability**: Whether you're developing a small indie game or a large-scale AAA title, the Shaga Environment SDK scales effortlessly to meet your project's needs.)

### Architecture
`ShagaSDK` is composed by three entities:
- `ShagaServerSDK`[[clone](https://github.com/ShagaDAO/ServerSDK)]: a fork of this [solana-labs repo](https://github.com/solana-developers/compressed-nfts), which exposes functionalities to games through a local http server written in `Nodejs` 
- `FrontEndDevSDK`[[clone](https://github.com/ShagaDAO/FrontEndDevSDK)]: a *Solana dApp* written in `Nextjs`
- `ShagaGameEngineSDK`: the GameEngine specific distribution
  - [ShagaSDK for Unity](https://github.com/ShagaDAO/CSharpSDK) written in `C#`
  - [ShagaSDK for Unreal Engine]( https://github.com/ShagaDAO/UEPluginSDK) written in `C++`

>Each `ShagaGameEngineSDK` opens a bi-directional `WebSocket` connection to the port `3101`, thus to the `ShagaServerSDK` entity.
>
>Each `ShagaDevFrontEnd` dApp opens a bi-directional `WebSocket` to the port `3102`, thus to the `ShagaServerSDK` entity.

![](./img/SDK_Architecture.jpg)

### Getting Started
To get started with the Shaga Environment SDK, after having cloned the two repositories mentioned above, do the following:

### `ShagaServerSDK`
Install `yarn` as packet manager, install packages and run the server.
```bash
  $ ~ npm install -g yarn   # install yarn globally 
  $ ~ yarn install          # install project packages
  $ ~ yarn dev              # run the server
```
This will print the following prompt:
```
Game Connection Listener started on port: 3101
FrontEnd Connection Listener started on port: 3102
```

### `ShagaDevFrontEnd`

```bash
  $ ~ yarn install  # install project packages
  $ ~ yarn dev      # run the frontend
```

Open http://localhost:3000 on the browser and connect your wallet through the UI.
![](img/Connect_Wallet.png)


### Support and Feedback
If you have any questions, feedback, or feature requests regarding the Shaga Environment SDK, please don't hesitate to reach out to us. We're committed to providing excellent developer support and continuously improving the SDK to meet your needs.

Thank you for choosing the Shaga Environment SDK. We look forward to seeing the incredible experiences you create with it!

Happy developing!