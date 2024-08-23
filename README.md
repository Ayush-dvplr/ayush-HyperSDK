# Customized Subnet Using HyperSDK

<p align="center">setting the constants in consts/consts.go</p>

<img align="center" width="581" alt="image" src="https://res.cloudinary.com/dsprifizw/image/upload/v1724434661/Screenshot_2024-08-23_230707_vtnphp.png">

<p align="center">Adding the code in registry/registry.go</p>

<img width="822" alt="image" src="https://res.cloudinary.com/dsprifizw/image/upload/v1724434661/Screenshot_2024-08-23_230718_v78170.png">

<p >launching the subnet using the following command.</p>

```bash
./scripts/run.sh;
```

if we don't need 2 Subnets for the testing, we can run

```bash
MODE="run-single" ./scripts/run.sh
```

<img align="center" width="1245" alt="image" src="https://res.cloudinary.com/dsprifizw/image/upload/v1724352863/hyperSDK_1_1.png">

By default, this allocates all funds on the network to `token1rvzhmceq997zntgvravfagsks6w0ryud3rylh4cdvayry0dl97nsjzf3yp`.

The private key for this address is
`0x323b1d8f4eed5f0da9da93071b034f2dce9d2d22692c172f3cb252a64ddfafd01b057de320297c29ad0c1f589ea216869cf1938d88c9fbd70d6748323dbf2fa7`.
this key has is also stored at `demo.pk`

To interact with the `tokenvm`, implement the `token-cli`.
Next, we'll need to build this. by using this command

```bash
./scripts/build.sh
```

This command will put the compiled CLI in `./build/token-cli`.\_

Lastly, we'll need to add the chains that we created and the default key to the
`token-cli`. we can use the following commands

```bash
./build/token-cli key import demo.pk
./build/token-cli chain import-anr
```

<img width="1113" alt="image" src="https://res.cloudinary.com/dsprifizw/image/upload/v1724352863/hyperSDK_1_2.png">

`chain import-anr` connects to the Avalanche Network Runner server running in
the background and pulls the URIs of all nodes tracking each chain we
created.

### Mint and Trade

#### Step 1: Create our Asset

let's create our own asset. You can do so by running the following command:

```bash
./build/token-cli action create-asset
```

When you are done, the output should look something like this:
<img width="580" alt="image" src="https://res.cloudinary.com/dsprifizw/image/upload/v1724434173/swarnali_hypersdk_1_mvk44o.jpg">

_`txID` is the `assetID` of your new asset._

The "loaded address" here is the address of the default private key (`demo.pk`). We
use this key to authenticate all interactions with the `tokenvm`.

#### Step 2: Mint our Asset

After we've created our own asset, we can now mint some of it. You can do so by
running the following command:

```bash
./build/token-cli action mint-asset
```

When you are done, the output should look something like this:

<img width="595" alt="image" src="https://res.cloudinary.com/dsprifizw/image/upload/v1724434173/swarnali_hypersdk_2_jw2gvn.jpg">

#### Step 3: View our Balance

Now, let's check that the mint worked right by checking our balance. we can do
so by running the following command:

```bash
./build/token-cli key balance
```

When you are done, the output should look something like this:
<img width="644" alt="image" src="https://res.cloudinary.com/dsprifizw/image/upload/v1724434173/swarnali_hypersdk_3_xglljj.jpg">

All the operations together.

<img width="729" alt="image" src="https://res.cloudinary.com/dsprifizw/image/upload/v1724434174/swarnali_hypersdk_4_bbjkif.jpg">

Apart from the above shown function our custom subnet can also perform following function.

#### Step 4: Create an Order

```bash
./build/token-cli action create-order
```

#### Step 5: Fill Part of the Order

```bash
./build/token-cli action fill-order
```

#### Step 6: Close Order

```bash
./build/token-cli action close-order
```

#### Watch Activity in Real-Time

```bash
./build/token-cli chain watch
```

### Transfer Assets to Another Subnet

```bash
./build/token-cli action export
```

### Running a Load Test

```bash
./scripts/tests.load.sh
```

#### Measuring Disk Speed

```bash
./scripts/tests.disk.sh
```

After all this we can stop our running subnet network by using:
to stop the network we started using
`killall avalanche-network-runner`.\_
