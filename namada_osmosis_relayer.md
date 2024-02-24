# Prepare test accounts:
```
namadaw derive --alias cybernova_se_acc
namadaw find --alias cybernova_se_acc
Found transparent keys:
  Alias "cybernova_se_acc" (encrypted):
    Public key hash: 8AF84A68C99542AD81F9B4E0A3AAF29597B59E6E
    Public key: tpknam1qzf3c3csf6x68tjemcjnwxyummcevds7647kx5fy0w2k0wkl962evjxv08k
Found transparent address:
  "cybernova_se_acc": Implicit: tnam1qz90sjngex259tvplx6wpga2722e0dv7dcr9xlzu
```  
```
osmosisd keys add cybernova_osmos_acc
  address: osmo1je2sa8rd2l8u40a05cvyu3fqachuspqajhec05
  name: cybernova_osmos_acc
  pubkey: '{"@type":"/cosmos.crypto.secp256k1.PubKey","key":"A5XfS7Oc+zoYeFspvDRaP7J3HrHpZ++2jBQSCtvQsTht"}'
  type: local

**Important** write this mnemonic phrase in a safe place.
It is the only way to recover your account if you ever forget your password.

spike warm earth way ordinary flavor essence leisure resource decide scan wet city yellow enforce chest open crime write van rookie poet draw three
```

# Add keys to Hermes
export HERMES_CONFIG=$HOME/.hermes/config.toml  

hermes --config $HERMES_CONFIG keys add --chain shielded-expedition.88f17d1d14 --key-file $HOME/.local/share/namada/shielded-expedition.88f17d1d14/wallet.toml 
```
2024-02-24T05:43:58.083589Z  INFO ThreadId(01) running Hermes v1.7.4+38f41c6
Enter your decryption password: 
SUCCESS Added key 'cybernova_se_acc' (tnam1qz90sjngex259tvplx6wpga2722e0dv7dcr9xlzu) on chain shielded-expedition.88f17d1d14
```
echo "spike warm earth way ordinary flavor essence leisure resource decide scan wet city yellow enforce chest open crime write van rookie poet draw three" > ./mnemonic   

hermes --config $HERMES_CONFIG keys add --chain osmo-test-5 --mnemonic-file ./mnemonic   
```
2024-02-24T05:44:50.972361Z  INFO ThreadId(01) running Hermes v1.7.4+38f41c6
SUCCESS Restored key 'cybernova_osmos_acc' (osmo1je2sa8rd2l8u40a05cvyu3fqachuspqajhec05) on chain osmo-test-5
```
# Configure Hermes
```
hermes --config $HERMES_CONFIG \
  create channel \
  --a-chain shielded-expedition.88f17d1d14 \
  --b-chain osmo-test-5 \
  --a-port transfer \
  --b-port transfer \
  --new-client-connection --yes
2024-02-24T05:45:37.918222Z  INFO ThreadId(01) running Hermes v1.7.4+38f41c6
2024-02-24T05:45:38.319335Z  INFO ThreadId(01) Creating new clients, new connection, and a new channel with order ORDER_UNORDERED
2024-02-24T05:45:54.927225Z  INFO ThreadId(01) foreign_client.create{client=osmo-test-5->shielded-expedition.88f17d1d14:07-tendermint-0}: 🍭 client was created successfully id=07-tendermint-1187
2024-02-24T05:45:57.317334Z  INFO ThreadId(01) foreign_client.create{client=shielded-expedition.88f17d1d14->osmo-test-5:07-tendermint-0}: 🍭 client was created successfully id=07-tendermint-2292
2024-02-24T05:46:08.521647Z  INFO ThreadId(01) 🥂 shielded-expedition.88f17d1d14 => OpenInitConnection(OpenInit { Attributes { connection_id: connection-515, client_id: 07-tendermint-1187, counterparty_connection_id: None, counterparty_client_id: 07-tendermint-2292 } }) at height 0-53624
2024-02-24T05:46:45.109788Z  INFO ThreadId(01) 🥂 osmo-test-5 => OpenTryConnection(OpenTry { Attributes { connection_id: connection-2168, client_id: 07-tendermint-2292, counterparty_connection_id: connection-515, counterparty_client_id: 07-tendermint-1187 } }) at height 5-5591631
2024-02-24T05:46:49.216629Z  WARN ThreadId(01) client consensus proof height too high, waiting for destination chain to advance beyond 0-53627
2024-02-24T05:46:49.747686Z  WARN ThreadId(01) client consensus proof height too high, waiting for destination chain to advance beyond 0-53627
2024-02-24T05:46:50.273008Z  WARN ThreadId(01) client consensus proof height too high, waiting for destination chain to advance beyond 0-53627
2024-02-24T05:46:50.790484Z  WARN ThreadId(01) client consensus proof height too high, waiting for destination chain to advance beyond 0-53627
2024-02-24T05:46:51.321685Z  WARN ThreadId(01) client consensus proof height too high, waiting for destination chain to advance beyond 0-53627
2024-02-24T05:46:51.849535Z  WARN ThreadId(01) client consensus proof height too high, waiting for destination chain to advance beyond 0-53627
2024-02-24T05:46:52.437834Z  WARN ThreadId(01) client consensus proof height too high, waiting for destination chain to advance beyond 0-53627
2024-02-24T05:46:52.981812Z  WARN ThreadId(01) client consensus proof height too high, waiting for destination chain to advance beyond 0-53627
2024-02-24T05:47:15.036348Z  INFO ThreadId(01) 🥂 shielded-expedition.88f17d1d14 => OpenAckConnection(OpenAck { Attributes { connection_id: connection-515, client_id: 07-tendermint-1187, counterparty_connection_id: connection-2168, counterparty_client_id: 07-tendermint-2292 } }) at height 0-53630
2024-02-24T05:47:29.392494Z  INFO ThreadId(01) 🥂 osmo-test-5 => OpenConfirmConnection(OpenConfirm { Attributes { connection_id: connection-2168, client_id: 07-tendermint-2292, counterparty_connection_id: connection-515, counterparty_client_id: 07-tendermint-1187 } }) at height 5-5591642
2024-02-24T05:47:32.432302Z  INFO ThreadId(01) connection handshake already finished for Connection { delay_period: 0ns, a_side: ConnectionSide { chain: BaseChainHandle { chain_id: shielded-expedition.88f17d1d14 }, client_id: 07-tendermint-1187, connection_id: connection-515 }, b_side: ConnectionSide { chain: BaseChainHandle { chain_id: osmo-test-5 }, client_id: 07-tendermint-2292, connection_id: connection-2168 } }
2024-02-24T05:47:48.088938Z  INFO ThreadId(01) 🎊  shielded-expedition.88f17d1d14 => OpenInitChannel(OpenInit { port_id: transfer, channel_id: channel-344, connection_id: None, counterparty_port_id: transfer, counterparty_channel_id: None }) at height 0-53633
2024-02-24T05:48:01.273696Z  INFO ThreadId(01) 🎊  osmo-test-5 => OpenTryChannel(OpenTry { port_id: transfer, channel_id: channel-5857, connection_id: connection-2168, counterparty_port_id: transfer, counterparty_channel_id: channel-344 }) at height 5-5591650
2024-02-24T05:48:20.132633Z  INFO ThreadId(01) 🎊  shielded-expedition.88f17d1d14 => OpenAckChannel(OpenAck { port_id: transfer, channel_id: channel-344, connection_id: connection-515, counterparty_port_id: transfer, counterparty_channel_id: channel-5857 }) at height 0-53636
2024-02-24T05:48:37.448651Z  INFO ThreadId(01) 🎊  osmo-test-5 => OpenConfirmChannel(OpenConfirm { port_id: transfer, channel_id: channel-5857, connection_id: connection-2168, counterparty_port_id: transfer, counterparty_channel_id: channel-344 }) at height 5-5591659
2024-02-24T05:48:40.462982Z  INFO ThreadId(01) channel handshake already finished for Channel { ordering: ORDER_UNORDERED, a_side: ChannelSide { chain: BaseChainHandle { chain_id: shielded-expedition.88f17d1d14 }, client_id: 07-tendermint-1187, connection_id: connection-515, port_id: transfer, channel_id: channel-344, version: None }, b_side: ChannelSide { chain: BaseChainHandle { chain_id: osmo-test-5 }, client_id: 07-tendermint-2292, connection_id: connection-2168, port_id: transfer, channel_id: channel-5857, version: None }, connection_delay: 0ns }
SUCCESS Channel {
    ordering: Unordered,
    a_side: ChannelSide {
        chain: BaseChainHandle {
            chain_id: ChainId {
                id: "shielded-expedition.88f17d1d14",
                version: 0,
            },
            runtime_sender: Sender { .. },
        },
        client_id: ClientId(
            "07-tendermint-1187",
        ),
        connection_id: ConnectionId(
            "connection-515",
        ),
        port_id: PortId(
            "transfer",
        ),
        channel_id: Some(
            ChannelId(
                "channel-344",
            ),
        ),
        version: None,
    },
    b_side: ChannelSide {
        chain: BaseChainHandle {
            chain_id: ChainId {
                id: "osmo-test-5",
                version: 5,
            },
            runtime_sender: Sender { .. },
        },
        client_id: ClientId(
            "07-tendermint-2292",
        ),
        connection_id: ConnectionId(
            "connection-2168",
        ),
        port_id: PortId(
            "transfer",
        ),
        channel_id: Some(
            ChannelId(
                "channel-5857",
            ),
        ),
        version: None,
    },
    connection_delay: 0ns,
}
```
# Test IBC transfer token back and forth
export BASE_DIR=$HOME/.local/share/namada   
export LEDGER="http://37.60.238.210:26657"  
```
namadac balance --owner cybernova_se_acc --node $LEDGER
naan: 1184.487509

osmosisd query bank balances osmo1je2sa8rd2l8u40a05cvyu3fqachuspqajhec05
balances:
- amount: "199988273"
  denom: uosmo
```

## Send naan to osmos via channel-344  
```
namadac --base-dir $BASE_DIR \
    ibc-transfer \
    --amount 2 \
    --source cybernova_se_acc \
    --receiver osmo1je2sa8rd2l8u40a05cvyu3fqachuspqajhec05 \
    --token naan \
    --channel-id channel-344 \
    --node $LEDGER \
    --memo tpknam1qzf3c3csf6x68tjemcjnwxyummcevds7647kx5fy0w2k0wkl962evjxv08k
Enter your decryption password: 
Transaction added to mempool.
Wrapper transaction hash: BEF96B148C902C8A6376716936DB14F148C7DA2C38B2347E80A89E4D00552FF6
Inner transaction hash: DE16681AE05D43598028ED52101B0FEF793B9DAF91A70B3D217742945D9FDCFA
Wrapper transaction accepted at height 53680. Used 26 gas.
Waiting for inner transaction result...
Transaction was successfully applied at height 53681. Used 6193 gas
```
```
osmosisd query bank balances osmo1je2sa8rd2l8u40a05cvyu3fqachuspqajhec05
balances:
- amount: "2"
  denom: ibc/2E5FBCB19E00000135A4BF3BC1BB67E34F3494193448D6A3DCE45278A4AB03EF
- amount: "199988273"
  denom: uosmo
```

## Send uosmo to Namada via channel-5857  
```
osmosisd tx ibc-transfer transfer \
  transfer \
  channel-5857 \
  tnam1qz90sjngex259tvplx6wpga2722e0dv7dcr9xlzu \
  1000000uosmo \
  --from cybernova_osmos_acc \
  --gas auto \
  --gas-prices 0.025uosmo \
  --gas-adjustment 1.1 \
  --node http://127.0.0.1:26657 \
  --home $HOME/.osmosisd \
  --chain-id osmo-test-5 \
  --yes
```
```
namadac balance --owner cybernova_se_acc --node $LEDGER
naan: 1179.987509
transfer/channel-344/uosmo: 1000000
```
