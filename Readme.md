# Hyper SDK Custom Subnet

## Description

This project enables the setup and execution of a **HyperChain** on the Avalanche network, utilizing Avalanche's **HyperSDK**. The project guides you through the initialization, configuration, and interaction with your custom HyperChain, featuring native tokens and smart contract actions like asset creation and minting.

## Getting Started

### Install Go

Follow this steps to install golang on wsl/wsl2

```bash
wget https://dl.google.com/go/go1.18.3.linux-amd64.tar.gz
sudo tar -xvf go1.18.3.linux-amd64.tar.gz
export PATH=$PATH:/usr/local/go/bin
```

Open .bashrc file and add following lines at the bottom and save the file.

```bash
export GOROOT=/usr/local/go
export GOPATH=$HOME/go
export PATH=$GOPATH/bin:$GOROOT/bin:$PATH
```

Check Go Version

```bash
go version
```

### Normalize Dependencies

Ensure all dependencies are up to date by running the following command in your project folder:

```bash
go mod tidy
```

### Configure Project Constants

In the `consts/consts.go` file, configure your chain by setting the `HRP`, `Name`, and `Symbol` values:

```go
const (
    HRP    = "AnkurChain"
    Name   = "Ankur"
    Symbol = "AC"
)
```

### Register Actions

Go to `registry/registry.go` and register the `CreateAsset` and `MintAsset` actions, which are responsible for creating and minting assets on your HyperChain:

```go
consts.ActionRegistry.Register(&actions.CreateAsset{}, actions.UnmarshalCreateAsset, false)
consts.ActionRegistry.Register(&actions.MintAsset{}, actions.UnmarshalMintAsset, false)
```

### Run the VM Locally

1. Ensure that Go is correctly set up on your path. If it is not, run one of the following commands to add it:

   ```bash
   export PATH=$PATH:$(go env GOPATH)/bin
   # OR
   export PATH=$PATH:/usr/local/go/bin
   ```

2. Build and run the project locally using the following commands:

   ```bash
   MODE="run-single" ./scripts/run.sh
   ./scripts/build.sh
   ```

### Load Demo Private Key

To interact with the blockchain, you'll need to load the demo private key included in the project:

```bash
./build/token-cli key import demo.pk
./build/token-cli chain import-anr
```

## Interact with Your HyperChain

Once the chain is up and running, you can start interacting with it.

### Mint and Trade

#### Create Your Asset

```bash
./build/token-cli action create-asset
```

#### Mint Your Asset

```bash
./build/token-cli action mint-asset
```

#### View Your Balance

```bash
./build/token-cli key balance
```

### Create an Order

```bash
./build/token-cli action create-order
```

### Fill Part of the Order

```bash
./build/token-cli action fill-order
```

### Close Order

```bash
./build/token-cli action close-order
```

### Close Your Local Avalanche Network

Once you are done, stop the local Avalanche network by running:

```bash
killall avalanche-network-runner
```

## Help

If you encounter any issues during the process, consult the project's README or run the appropriate command for help.

## Authors

- **Ankur Pandey**

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.


