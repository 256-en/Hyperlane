# Hyperlane-Bridge
Hyperlane, geçtiğimiz günlerde dev odaklı bir airdrop yapacağından bahsetti. User tarafı da uzun süredir şişmekteyken bu tarafta birkaç basit işlem yapalım.

## # Updates
```console
sudo apt-get update && sudo apt-get upgrade -y
apt install curl iptables build-essential jq git make gcc nano wget htop tmux pkg-config nvme-cli libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip libleveldb-dev -y
```

## # nvm
```console
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash

export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"

# Node.js && npm && yarn
nvm install node
npm install -g yarn
```

## # Hyperlane
```console
git clone https://github.com/hyperlane-xyz/hyperlane-monorepo.git && cd hyperlane-monorepo && yarn install && yarn build && cd typescript/cli

# Bir EVM wallet oluşturun, private key kaydedin. 
# içine Base Ağında 0.0025 $ETH, Zora ağında 0.002 $ETH atın. 
# İşlemler için yaklaşık 1-2$ harcayacak sonra çekebilirsiniz.

export PVT_KEY="Private Keyinizi girin, Tırnaklar kalsın"
export WALLET="Cüzdan adresinizi girin"

export HYP_KEY="$PVT_KEY"

mkdir -p ./configs

# cat komutuyla başlayıp ikinci EOF ile biten arayı toplu girin.
cat <<EOF > ./configs/warp-route-deployment.yaml
base:
  interchainSecurityModule:
    modules:
      - relayer: "$WALLET"
        type: trustedRelayerIsm
      - domains: {}
        owner: "$WALLET"
        type: defaultFallbackRoutingIsm
    threshold: 1
    type: staticAggregationIsm
  isNft: false
  mailbox: "0xeA87ae93Fa0019a82A727bfd3eBd1cFCa8f64f1D"
  owner: "$WALLET"
  token: "0x532f27101965dd16442e59d40670faf5ebb142e4"
  type: collateral
zoramainnet:
  interchainSecurityModule:
    modules:
      - relayer: "$WALLET"
        type: trustedRelayerIsm
      - domains: {}
        owner: "$WALLET"
        type: defaultFallbackRoutingIsm
    threshold: 1
    type: staticAggregationIsm
  isNft: false
  mailbox: "0xF5da68b2577EF5C0A0D98aA2a58483a68C2f232a"
  owner: "$WALLET"
  type: synthetic
EOF

yarn hyperlane warp deploy

# Terminaldeki son çıktıyı -ağları içeren-  kopyalıyoruz.
```

## # Bridge
> Adresinizi relayer olarak tanımladınız. Köprü için bize biraz token lazım.
> Base <> Zora arasında köprüleyebileceğiniz $BRETT tokenı var. Uniswap üzerinden alabilirsiniz.

> Sonrasında https://hyperlane.superbridge.app/ adresine gidiyoruz. Normalde Zora Ağı gözükmeyecektir, nasıl ekleyeceğinizi videoda anlattım, oradan devam edebilirsiniz.

> Takıldığınız bir yer olursa: ▪️ X : https://x.com/256_tr ▪️ X : https://x.com/256__en
