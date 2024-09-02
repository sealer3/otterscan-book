# Running Otterscan on Pectra devnet-2

At the time of this writing (Aug 2024), the next expected Ethereum hardfork is **Pectra** and **devnet-2** is up.

> 💡 This document may be updated for future devnets as Erigon becomes stable enough to sync them.

It is possible to run Otterscan against this devnet with some known limitations.

- Pectra-specific features are still in development in Otterscan. Otterscan should work fine, but EIP-7702 transactions may not display correctly or may generate UI errors, for example.
- It requires a dev build of Erigon 3 alpha.
- Caplin (Erigon internal CL) still doesn't support Electra. For CL, it requires a dev build of Lighthouse.

## Get the chainspec

- Checkout the `pectra-devnets` repository.
  ```shell
  git clone https://github.com/ethpandaops/pectra-devnets
  ```
- Set `$PECTRA_DEVNETS` to be this `pectra-devnets` directory.

## Run Erigon

- Checkout and build the `docker_pectra` branch of Erigon.
  ```shell
  git clone -b docker_pectra https://github.com/erigontech/erigon
  cd erigon
  make erigon
  ```
- Initialize the chaindata with the devnet-2 spec. Consider `$ERIGON_DATADIR` to be the EL datadir.
  ```shell
  build/bin/erigon init --datadir=$ERIGON_DATADIR $PECTRA_DEVNETS/network-configs/devnet-2/metadata/genesis.json
  ```
- Run erigon as usual.
  ```shell
  build/bin/erigon \
    --datadir $ERIGON_DATADIR \
    --networkid 7011893082 \
    --bootnodes="enode://11cad2febebbb604b28ab4714988bb56b7cd3508edfe8ec4d62f15ba83d688cfe788dab311b43de082ef0b40a24d877cbb4129dee960af8d1d5a228a9805c684@46.101.214.247:30303?discport=30303,enode://07887f763e2be15de66a653e84cb4fc65ed6203e023d34e79b41e3f8baf957c956995408df8654a1acac20d12b46338638be096dafdb323239918c693c4b9aa5@178.128.198.156:30303?discport=30303,enode://3bf7e2d3c4d8784380da93023b5e3f49974a5857ba0adfa51bdc6b9375b21ecb0cbef4a0ee288c570ec6c0744d63d9f966f171a4f148707ad9461f8911245e29@207.154.235.122:30303,enode://c04d6cc9206e54284151d5ef67109505a837dd6954c6415e836e2913bc69c5664c95e8da90110972a78bfd627165134683fa5231b64263a79bdc57c0f861e555@139.59.209.140:30303?discport=30303,enode://4a0410e481e97cff53a983947228162c4a314f8ff732884b78965407c7dcfa3ee77d2c25ad4247f5dffcbe1b93b11f544c36dde00c51165a3df48e358ff51b43@167.99.250.53:30303?discport=30303,enode://c8f46212b1da135f7de335c91357741f4e9f1e8fd48b9f1726440e2a8b3d62e5e55d9fe23dd40b2eb638c4b65d09dd5cd1689d01be0136a18d5cc4aeb6a77800@178.128.193.102:30303?discport=30303,enode://7059ac21a06edabc984570139a8f34370c0361d0c0edca7458df9e705540f1a00a95287eb95024cf62a389e13e71e31a586141af9662c7bbb068336fb1e20a5a@157.230.113.198:30303?discport=30303,enode://dd1067e7016d157ed4ae17556ad575fb532f5c86c97f92b21e89eca34da62b2f8ad98d85303e441596ee9abfafc05f52a0b123650f8bdce3e0de528d9f318514@64.226.65.123:30303,enode://1ae87a905cd8a258a4da5fe7b47348c5b7f02fcbefaab68886bc05f7eb6584ff3d8122e572a864c0e7d72cf8876affe5dc3920a152c3ffe97fe4e2d3cd7b0c69@164.92.238.47:30303?discport=30303,enode://667dcf4ba1185f5be82f9ca2888da760effc119d6d55f29c44532356cc448ed7d46fc12ae5fbc169777559b77eef7aed0fdabc4d1106a8eda7820654219203e5@104.248.132.55:30303?discport=30303,enode://6de16972bf1d7de11da2e0472196c084b9e284f3aa7d5414083b74e7dc3a36118e0a41b39a78bcd5bf8a2ddfd4a8cb3ca6438abb163b0c6d020761438c26686a@165.232.114.61:30303?discport=30303,enode://37590f6f8ca0a5f1f14d8e83fbd19379dc7dc4978614a4cdd04ab0c7cd966c8279994c190d9eada2575f3b335a44518cba2811fd62a84165f5f17072854a72eb@164.92.186.171:30303?discport=30303,enode://740b829c620c9319809528d248f4b92b72032703344f2c2de98c7d3dfe48ab4328db7d5fe3b016f29c8ec1ba864ac5bffaee04b4f035fc15e872caff102ec1cb@157.230.19.81:30303,enode://516f3449e085da319a6a345b75378d15c8eb8444769f325c1dd1bb60cf1f0c7bf50e471ade38db90800db345a5594b1822a5bf2c6086c814c9ddcd752db1b218@167.99.143.103:30303?discport=30303,enode://848d233aca20a13d4678eb333e17abb666365f176891204619b952e06a837a911075a1423eaab1ea2a5b86e19bba5bb59bf24ff65509bd3a726e7240f72c265c@68.183.76.162:30303?discport=30303,enode://4e282ae804e098094415e84a4681b353e075439b739197e80fc0a6bb045c2ecc77fedea82bb2dd9e85bbb9dc0f9d6edc905e73a9e31ad669aca6b320b271f02d@209.38.200.135:30303?discport=30303,enode://702ea45e86923c650c0c4321aae30ef783f7ab4954939ed29d155b8a5ed72aa078bbe6ab7f46c042450616c89c27d3526572a83cf650bdb30d02ecb532437c24@157.230.19.137:30303?discport=30303,enode://a25afb6cec454e3d6b2aa27f56d3ba76dd601541087d2af206fb9c235356e2e07c7f9642b30e29ddd6f6e48eb4cfac4aa76f9bf02ebb32f2c0a5da3556679ead@165.227.168.193:30303,enode://236536c973b101f6917e6a97c691e292148d7ee161508de97fc8783e53f7cc3ff3045f34a0b042690b69490b07ac64fe81386deb19998333c993f2e48d3fe245@207.154.246.51:30303?discport=30303,enode://e7551c56f0b179b256db8b80ab41726bbdd0fff078c75e3cacc026bcc677d6d72ee9dc6b76d6ecfc5dd2dc34af1d6ce03c654cc231f30690a77beb44ec9ed184@207.154.205.114:30303?discport=30303,enode://242f7e3f4f59d0c5a7e861702bc7130897c4fd4781b05a3dda0f5b9ccdae9dac523ba8166d9ddf36408b165212f84290ee14780373f2b45a89a4fd4271d767c5@165.22.85.81:30303?discport=30303,enode://e4c91e83e05aa32efba984409bde029c30a82ae4485c8b4c6da19fff033bfaf6f4e6add52264944d50ff86fa34be2edb7534170b07e77403774f2b5e58830e09@159.89.3.86:30303?discport=30303,enode://46eeae40981899766d2637300e8883db3261967c357691d7cb3779562afc3170cebd350dbcb1a7ea06746eeb019ddcd33bc9a8c9c629fb76145d3fc3da362584@164.92.128.193:30303,enode://b8abc384c3fa52f11659cc308870d6c9e85d5329e6d4f5b0d5c6dd55e3f68d593505feee383d2d04cc15c10bd67c1f16f003061f87fb33347424ca1b3e60422c@46.101.215.88:30303?discport=30303,enode://6a9fa2cbcb1b194e96052bb24f53f5f31f78a68f4954d89c5f02ab7a3cf75d2a2778de8443dd99613243fd1b37d66ce4585cab621fb0ce61a6b3fbd2ea37589e@207.154.231.130:30303?discport=30303,enode://f31c349ee4ddf983569ec47bd40082ce0b8135041082fe0a8ced48d13af6ec7e4d1a5a378d483d549498cde84e444a2025de1086565a6868965545ac409307c5@207.154.231.127:30303?discport=30303,enode://52524527bceb975747dcb25af270e9bcce69eb047c467a50756a7c794573b2c095675995c6d4106266392dc3624e889537de1811a81013084c8c9af06610ea6e@165.227.128.224:30303?discport=30303,enode://ed5b146b7ccba3e92091e06fa396317cdf264db0908a02003155a6fe40d98974f49efb2790c38fd7ba76c4d9a223171eb00a63fc2dc62d4b962288845c7593cf@134.209.225.88:30303,enode://689e7907e7e1399fe3f0d0c9309cb5e609ffcc0ec7f1516b9a0798870134ed60f336db28004e137015fc25b799e9cccb646c2a8dec9090d160f3be997e9bf8e7@157.230.107.247:30303?discport=30303,enode://4377de59b3703e8641d96ba5dfdaae6f212f63371401414486308c5bd763c95fcae50bc1458debeddc5a5e0980b814ed868c4b5b0e80f6141dd77069787f69ee@46.101.215.10:30303?discport=30303" \
    --externalcl \
    --http.api "eth,erigon,ots" \
    --http.corsdomain '*'
  ```

> Note: the bootnodes are taken from [here](https://github.com/ethpandaops/pectra-devnets/blob/master/network-configs/devnet-2/metadata/enodes.txt)

## Run Lighthouse

- Check out and build the `unstable` branch of Lighthouse.
  ```shell
  git clone -b unstable https://github.com/sigp/lighthouse
  cd lighthouse
  make
  ```
- Run lighthouse as usual. Consider `$LH_DATADIR` is the CL datadir.
  ```shell
  target/release/lighthouse bn \
    --testnet-dir $PECTRA_DEVNETS/network-configs/devnet-2/metadata/ \
    --datadir $LH_DATADIR \
    --allow-insecure-genesis-sync \
    --execution-endpoint "http://localhost:8551" \
    --execution-jwt $ERIGON_DATADIR/jwt.hex \
    --boot-nodes="enr:-Iq4QIRjFPzLFzd_U6pxxMSceIIoNwxGP4PlgW47QrAt5R_LF5JZDzYrWN41U4Oe1IwxsM6s0xNIPPcSBQTDngTYDnmGAZEC2n76gmlkgnY0gmlwhES3TDSJc2VjcDI1NmsxoQJJ3h8aUO3GJHv-bdvHtsQZ2OEisutelYfGjXO4lSg8BYN1ZHCCIzI,enr:-LK4QIOatlWDCVuZmAlrgWp6AIXq_c-TAxlmfUG8SabrbT-OC19a6pdURZjiAS19v4QVctuxMbxkfXQHJj4wvEoBqjEEh2F0dG5ldHOIAAwAAAAAAACEZXRoMpCvgSqQYEWHOQIAAAAAAAAAgmlkgnY0gmlwhES3TDSJc2VjcDI1NmsxoQMurKOrgb0FqbTRQvQJFPBGScdfdHeBmO5sdlYqlUb2MYN0Y3CCIyiDdWRwgiMo,enr:-MS4QPMg1GOyxmTco6OVowI1jmL-xveXdqoMOvwHeoT7gVfCWvu9-UG37NxDSljN5A1CZNLhrwTP7oFVY96FBubevUQBh2F0dG5ldHOIAAAAAAAAAACEZXRoMpCvgSqQYEWHOQIAAAAAAAAAgmlkgnY0gmlwhC5l1veEcXVpY4IjKYlzZWNwMjU2azGhA9SccDblrBX4KJTppdRjbA2qVALSKkBUDmEeByCMuprtiHN5bmNuZXRzAIN0Y3CCIyiDdWRwgiMo,enr:-MS4QFgoSWy-t9BFMm5EXTwPr2feV-Izm0XCE2dXrWkic9V2BqRdWBuu5cxmWxl6syNX_IlUEbKaNoT51aRFebTbXgIBh2F0dG5ldHOIAAAAAAAAAACEZXRoMpCvgSqQYEWHOQIAAAAAAAAAgmlkgnY0gmlwhLKAxpyEcXVpY4IjKYlzZWNwMjU2azGhAhOSWIeBetNaVfeBVipsE-9VUIfVsgtfgESltZSznNYpiHN5bmNuZXRzAIN0Y3CCIyiDdWRwgiMo,enr:-MS4QCbrmO2CvU2icdPBFQ8pS1twaR0BHa9HKNPpv1ckp-RoVNQqrbWeafexD6geUq8rmssTTzI6H5R7xCGNTYSpiAwBh2F0dG5ldHOIAAAAAAAAAACEZXRoMpCvgSqQYEWHOQIAAAAAAAAAgmlkgnY0gmlwhM-a63qEcXVpY4IjKYlzZWNwMjU2azGhAo5xBQ33UNmqp4FRxAV5ZqaMmSjx4kvZe2j9ctRx8AjqiHN5bmNuZXRzAIN0Y3CCIyiDdWRwgiMo,enr:-MS4QPekInz4EYD3abBpv-7_1C5iX1NVfjVbpCsI-p7fHnCHQohMtXk1oQ8YfuQSFVEOXcsHAVg7_VavZ_YgIQ6AaTkBh2F0dG5ldHOIAAAAAAAAAACEZXRoMpCvgSqQYEWHOQIAAAAAAAAAgmlkgnY0gmlwhIs70YyEcXVpY4IjKYlzZWNwMjU2azGhAr-5nuLB1eY1qxPH8xkWP_dR0jCNxuTEndcc_xWvB66HiHN5bmNuZXRzAIN0Y3CCIyiDdWRwgiMo,enr:-MS4QMh-KWyNyk9GzBXbVOR1slwaBFbYJ3rn4roTrvjrBu0hWOJaeIXNCoUskoJEXFzNbcfmXQjPHO4x37khPr63fKwBh2F0dG5ldHOIAAAAAAAAAACEZXRoMpCvgSqQYEWHOQIAAAAAAAAAgmlkgnY0gmlwhKdj-jWEcXVpY4IjKYlzZWNwMjU2azGhAicdfO311fGEsvTam0JQFL_YIiDw2LIHr4yKdTabkl0ZiHN5bmNuZXRzAIN0Y3CCIyiDdWRwgiMo,enr:-MS4QJnbYQcJgMnyqi5ODw6W78jVnc4FzVOsP7mp9o2Tbsa5bSZbgM4M7YtXuBWROxtk-A6gL7QWGGjoCxa4n6RaP1oBh2F0dG5ldHOIAAAAAAAAAACEZXRoMpCvgSqQYEWHOQIAAAAAAAAAgmlkgnY0gmlwhEDiVgqEcXVpY4IjKYlzZWNwMjU2azGhAoEI_xevRhmXp7tArVuP0DRzX5VjSO6XgCUTL-hZyRQLiHN5bmNuZXRzAIN0Y3CCIyiDdWRwgiMo,enr:-MS4QMix3VOMlmD__42OgsxoVV-KqSIhl1VOjz1vFhagsorneZWnOLWi0F7D5N_VAxi7Ty_LJ7HPfCXTs-ggQHYabV0Bh2F0dG5ldHOIAAAAAAAAAACEZXRoMpCvgSqQYEWHOQIAAAAAAAAAgmlkgnY0gmlwhLKAwWaEcXVpY4IjKYlzZWNwMjU2azGhAngUhQb4hgqkCWx7Wrkq7spxUihumcrtzIVkvI7t6CCliHN5bmNuZXRzAIN0Y3CCIyiDdWRwgiMo,enr:-MS4QBzWNcy1PHFa9BGnlXzXG8TtpOSwfkdbvA8zyoUpqgKZPs00SpC_WaEluhFP0TTkvDgKGH9kI9aDhKneQ0m8H54Bh2F0dG5ldHOIAAAAAAAAAACEZXRoMpCvgSqQYEWHOQIAAAAAAAAAgmlkgnY0gmlwhJ3mccaEcXVpY4IjKYlzZWNwMjU2azGhA9abbABNaJg1txVss_-xmHH71Sa8OTZuH_E-qWU6ADqNiHN5bmNuZXRzAIN0Y3CCIyiDdWRwgiMo,enr:-MS4QOcQwXvRxw8EE_2YbkP0b18_c5AyH8rXzJKVX4waQaEaWIyI0OMnUEQdqlxNPJc6qMJNVrjPUa46L2ik95EILPwBh2F0dG5ldHOIAAAAAAAAAACEZXRoMpCvgSqQYEWHOQIAAAAAAAAAgmlkgnY0gmlwhEDiQXuEcXVpY4IjKYlzZWNwMjU2azGhAvJmg_fEum7uTDsGLV62ByfQJc-lx263gQvaBK5s2y5FiHN5bmNuZXRzAIN0Y3CCIyiDdWRwgiMo,enr:-MS4QAdbt3MrSmwFuDBGv05x8kn5QN9f7kfoCEkr9-Ga1tElHpVlf0vnwezJLHsnXEJP10YkpylBvPu8iW_zWKBTWZoBh2F0dG5ldHOIAAAAAAAAAACEZXRoMpCvgSqQYEWHOQIAAAAAAAAAgmlkgnY0gmlwhKRc7i-EcXVpY4IjKYlzZWNwMjU2azGhAz_ZGRHlNWMAPNaLLaimAdlQx_7UkFUQL-JS1wa9v9W9iHN5bmNuZXRzAIN0Y3CCIyiDdWRwgiMo,enr:-MS4QNLwvwmihiJP5AFp6D_rEvxf1pmT42NKirZWQfyhu6PRZXrr9sxvXtIfnZyAeJHmfdqY0V4mhgZf7W9yCEgrfkcBh2F0dG5ldHOIAAAAAAAAAACEZXRoMpCvgSqQYEWHOQIAAAAAAAAAgmlkgnY0gmlwhGj4hDeEcXVpY4IjKYlzZWNwMjU2azGhAkwIMB90Y5Pv8Bqie1AxL4uiH1cH_79x2Lzx0Epr7ASIiHN5bmNuZXRzAIN0Y3CCIyiDdWRwgiMo,enr:-MS4QGoR9HGz4pyy8zfwsfYaQXAmLwz-lQmJCmIZMP3ng0ElBSBC6FpD4jgz0ZLkHfPRtEsGFZRLpkEAMwRsV14ixfYBh2F0dG5ldHOIAAAAAAAAAACEZXRoMpCvgSqQYEWHOQIAAAAAAAAAgmlkgnY0gmlwhIbR-2uEcXVpY4IjKYlzZWNwMjU2azGhAluLNJAaCmGLGWdGwiN-LMrxiQpUEZEmkb1b9dpFGie-iHN5bmNuZXRzAIN0Y3CCIyiDdWRwgiMo,enr:-MS4QFFhYGp00jI1pm4Ao6uMLrler8IeD5fh_FGifQFGPLeLVP90oIofFcvi_47NC1Cs3hjHpuHD_GGP3Pov5MdnywUEh2F0dG5ldHOIABgAAAAAAACEZXRoMpCvgSqQYEWHOQIAAAAAAAAAgmlkgnY0gmlwhKXocj2Jc2VjcDI1NmsxoQPDVjkFouaNfb998j95T1ZTSKaf-PSqpP2CDEU6-ky3r4hzeW5jbmV0c4gAAAAAAAAAAIN0Y3CCIyiDdWRwgiMo,enr:-MS4QG5K8sCjXoLrcbSP6cG083ZWU0u2IUhubivV6khMVzFaDo9JPMRt_ek5-bLhyF4YZj2y6Qs8HMZHOJA_Ks53BDUEh2F0dG5ldHOIAAAAAACAAQCEZXRoMpCvgSqQYEWHOQIAAAAAAAAAgmlkgnY0gmlwhKRcuquJc2VjcDI1NmsxoQNpD9ViCM_Jf8No8JuG78TN2R-43q45maP7b3l5FDFzfohzeW5jbmV0c4gAAAAAAAAAAIN0Y3CCIyiDdWRwgiMo,enr:-MS4QLNvfCzl9C1tmmEcqv2EXMg4uDieKUj01CUSJx3KxGisO2pIXj_KgHXtZ7xs5eJcjUgdH3Mtd2J4AUGW9DiUt2UEh2F0dG5ldHOIAADAAAAAAACEZXRoMpCvgSqQYEWHOQIAAAAAAAAAgmlkgnY0gmlwhJ3mE1GJc2VjcDI1NmsxoQJPKIIDUWVXJoMIqOkrYyQ2O1OoJ95FlzsscSULR9tG6YhzeW5jbmV0c4gAAAAAAAAAAIN0Y3CCIyiDdWRwgiMo,enr:-MS4QJV9mzMPwWTDhUjcAfJmJ5yRDTtqB_Wta0v9dQD0vbjOBktmKyXh1yT5yQysQIjWvttnovFSS12lXmiCmAREIkgEh2F0dG5ldHOIAAAMAAAAAACEZXRoMpCvgSqQYEWHOQIAAAAAAAAAgmlkgnY0gmlwhKdjj2eJc2VjcDI1NmsxoQOoq9_cfpB6FJag8Gea9d5W4DD-AoxUQx21WUQTIvUQp4hzeW5jbmV0c4gAAAAAAAAAAIN0Y3CCIyiDdWRwgiMo,enr:-MS4QMipihRjrOsw3WF5dMZQVdrR28soeATGctTl-VnEMlCVNZOuxIaiGDI20sm3tjUf4L0qpYn9Awc2mah1-JJINusEh2F0dG5ldHOIAAAAAAAAMACEZXRoMpCvgSqQYEWHOQIAAAAAAAAAgmlkgnY0gmlwhES3TKKJc2VjcDI1NmsxoQKGIh5ia10cMh0ZUt8zjxO7QxoEm60aSmdm66hhOglHsIhzeW5jbmV0c4gAAAAAAAAAAIN0Y3CCIyiDdWRwgiMo,enr:-MS4QEkHM-F7L_P6gQEZ71d7zF9jWnPtl-WMeSblQ3wP8m2tI3BLvTM6rO-a1O68XWVSjjq2HcEcpAw1i40BaTDaVUcEh2F0dG5ldHOIAAAAAAAAMACEZXRoMpCvgSqQYEWHOQIAAAAAAAAAgmlkgnY0gmlwhKEjyNiJc2VjcDI1NmsxoQLMGowFEgNZ0hkluwDV5MGGdTKhyOVcHZ_O2wDymmY7CohzeW5jbmV0c4gAAAAAAAAAAIN0Y3CCIyiDdWRwgiMo,enr:-Ly4QGTdhF0AhUC7cfKv92fJKK758XEwLNkMxc9eP_udVDCUYPAYRz4IZjo1E1-CAL2GPymX2WM_t46iGpTUmN6jbTcDh2F0dG5ldHOIAAAAAAAYAACEZXRoMpCvgSqQYEWHOQIAAAAAAAAAgmlkgnY0gmlwhNEmyIeJc2VjcDI1NmsxoQPZnq3pyfkc62kLWGqaBjtND-0tj4QaZF5qPGtEbzjeg4hzeW5jbmV0cw-DdGNwgiMog3VkcIIjKA,enr:-Ly4QOkaE8ul01m7lXTN_O871JpwA8RkNjtz8gJs8ifc1YHoFIut7Lr4bI9SB0QK9NqCeQiouH-W1JdEoC--BlmwZMYDh2F0dG5ldHOIAAAAAAYAAACEZXRoMpCvgSqQYEWHOQIAAAAAAAAAgmlkgnY0gmlwhJ3mE4mJc2VjcDI1NmsxoQMfjSHypHchTnwZ3rxRUdNQ6zJhAkcZL8fexoZC14J2NYhzeW5jbmV0cw-DdGNwgiMog3VkcIIjKA,enr:-Ly4QBhVN2P5j23oiU2F2pxbPBOqTDQFtlIh_CSBQi4zXJEuTJk-SooV1BQcrrd9bY1hM9u3VH_Nckztix8hEWDKwDoDh2F0dG5ldHOIAAwAAAAAAACEZXRoMpCvgSqQYEWHOQIAAAAAAAAAgmlkgnY0gmlwhKXjqMGJc2VjcDI1NmsxoQPqJYtrQqlDhFz0TxUbHx6FrzHTCbH8RuN5sUnard2JsohzeW5jbmV0cw-DdGNwgiMog3VkcIIjKA,enr:-Ly4QO05d0xxKbtNd1ixJGbiSSyZ57C_cQNRptg7vTyyajdhRKkJcQb04tQ9I3x42q5xy1SHVSlhFA-928k4IdK_8yMDh2F0dG5ldHOIAAAABgAAAACEZXRoMpCvgSqQYEWHOQIAAAAAAAAAgmlkgnY0gmlwhM-a9jOJc2VjcDI1NmsxoQMfR97ZxMFFVQkTf-9vF0zoNWjtQcFnYvhMPknUscJsgYhzeW5jbmV0cw-DdGNwgiMog3VkcIIjKA,enr:-Ly4QBpjEu3cMMDOr0MzR1eDxSrUwk8Kvd8f-bm9EFNVY_p-TH9TtXqo8RlXO4UHexXD4SUWps5BOobozTDYjPsgWYEDh2F0dG5ldHOIAAAAAABgAACEZXRoMpCvgSqQYEWHOQIAAAAAAAAAgmlkgnY0gmlwhM-azXKJc2VjcDI1NmsxoQPO3G_mrYDC5nbWN5hCQrjUzoRKAy0tlcCzmziV18JdC4hzeW5jbmV0cw-DdGNwgiMog3VkcIIjKA,enr:-Ly4QJG8cHFEWXAMtfC3eLkjtQSK3-CYq6FXgR4bUSGc0ABpWJUS95jnmuK4mKlhmAhmVv2YkPzcWu7ezS-XWu6bfqQDh2F0dG5ldHOIAACAAQAAAACEZXRoMpCvgSqQYEWHOQIAAAAAAAAAgmlkgnY0gmlwhKdHLU-Jc2VjcDI1NmsxoQKcRN8oZsaP2KiEt_7ldpfQiH8WdgGPk7gZbJoaGEEezohzeW5jbmV0cw-DdGNwgiMog3VkcIIjKA,enr:-MK4QJZWcLsrQA9OFZ2Qw_e_iccz4-qYJWAYU5UtEFEqXK9uZrNvglZcNamk488IZBWjKLZsHUn0VgQH7o9N9WrprpOGAZEC_Njbh2F0dG5ldHOIAAAAAAAAgAGEZXRoMpCvgSqQYEWHOQIAAAAAAAAAgmlkgnY0gmlwhKUWVVGJc2VjcDI1NmsxoQImk59RSNNYMkqydC3JLJdZJ2blx4h5fO2dZeA8zcblx4hzeW5jbmV0cw-DdGNwgiMog3VkcIIjKA,enr:-MK4QDRBGMCVLTCYAe9wcPYg__D4KUp0wbqWP1b22OEWnhyge10VnnGTj7ITkoxqD7E19N2Kys25RDD__Y_UTjxNufqGAZEC_Negh2F0dG5ldHOIDAAAAAAAAACEZXRoMpCvgSqQYEWHOQIAAAAAAAAAgmlkgnY0gmlwhJ9ZA1aJc2VjcDI1NmsxoQJluTr4qdAWQ39QbZ0RgVcizoEtuiaXJXTCXUPlz1LQGIhzeW5jbmV0cw-DdGNwgiMog3VkcIIjKA,enr:-MK4QB1uPkXKWMdsmB27AgygNxI4ySzCGxR3QtvYGYEhS2qeKaao5_2zteymUjrbUcsLZ6AIuZWgKSZU_4KRj6q1fPuGAZEC_NeIh2F0dG5ldHOIAABgAAAAAACEZXRoMpCvgSqQYEWHOQIAAAAAAAAAgmlkgnY0gmlwhKRcgMGJc2VjcDI1NmsxoQJqUAzY2v_Q0DUoLlLlhpCipdyTeBr2aDaTSj-WJzWZd4hzeW5jbmV0cwuDdGNwgiMog3VkcIIjKA,enr:-MK4QN5ynTLsXRtFblGBk0mKiT8OraO4lta10M1yxWH-RnVVSET4wkRNBoEUaH7htTT28JkrBM4Sn88rXH9RS08a_wKGAZEC_NfAh2F0dG5ldHOIAAYAAAAAAACEZXRoMpCvgSqQYEWHOQIAAAAAAAAAgmlkgnY0gmlwhC5l11iJc2VjcDI1NmsxoQN_bdnjvsT0fpEtYopA6h4QDDUZoiwZt7hbTruiiLCShohzeW5jbmV0cweDdGNwgiMog3VkcIIjKA,enr:-MK4QFaXKTrhtkPQxXQ7wFfk7QMFigd8gKdlGsN_8n8Yv_GvWGKPFLpWLf_mhAX-2aRXPo_WMkHvy0rgYBfUOo3VrkmGAZEC_Nd9h2F0dG5ldHOIwAAAAAAAAACEZXRoMpCvgSqQYEWHOQIAAAAAAAAAgmlkgnY0gmlwhM-a54KJc2VjcDI1NmsxoQLVovxnIoEiyxZKtR97N2cmbIAAhlGEFwEjckZzWt0z34hzeW5jbmV0cw-DdGNwgiMog3VkcIIjKA,enr:-MK4QFvauosLiVzMbEYTB9N0-SB8Qvi63tNeexGykvDiOkDgKSQ422yNJzmTiXddo7w26lv09l36pkkVseo9Zs2BTxSGAZEC_Nhuh2F0dG5ldHOIAAAAAMAAAACEZXRoMpCvgSqQYEWHOQIAAAAAAAAAgmlkgnY0gmlwhKXjqXaJc2VjcDI1NmsxoQJt2NxZ4sBSZ0VmDAfhhQzkufQDmUdCsybUmvvW17rAcIhzeW5jbmV0cw-DdGNwgiMog3VkcIIjKA,enr:-LK4QE1N5PWvOa8Ym-kH2jmqN8_4_8K8MFfIfXPXdV0x8DPcBjHDJWznTMDbtTENxfhSK_geEN02HKKYbkG2S_XjnycEh2F0dG5ldHOIAGAAAAAAAACEZXRoMpCvgSqQYEWHOQIAAAAAAAAAgmlkgnY0gmlwhM-a53-Jc2VjcDI1NmsxoQK94Sc-fPbGJW75YzdIYabZ90EbbFAV337Q8XFIishpe4N0Y3CCIyiDdWRwgiMo,enr:-LK4QG_-Y5VSaVNIparcx2_3iom49xVQqb0_8naFE8TySYnVfZ3nmSoCycD4TMkHcKWQXQVpmrjH8OfIqWuHxHv6KskEh2F0dG5ldHOIAAAAAAAwAACEZXRoMpCvgSqQYEWHOQIAAAAAAAAAgmlkgnY0gmlwhKXjgOCJc2VjcDI1NmsxoQK_gDI7yRZanIFmml3e-kDjYBH-7PDYtTGCbMwUUnlMv4N0Y3CCIyiDdWRwgiMo,enr:-LK4QCCp9-BI-AxZ6R2sAmGymW3wOGiudMskeKkCYkTVrCpSR-TpmTy-QD4jH7Pp9FJo0VmkKKicJ6BCBewwy9f2qF0Eh2F0dG5ldHOIAAAAAAAAMACEZXRoMpCvgSqQYEWHOQIAAAAAAAAAgmlkgnY0gmlwhIbR4ViJc2VjcDI1NmsxoQPHxYBsTw1DUW25YyB2exSwfqgq2Bjxhr1ire7722P5BYN0Y3CCIyiDdWRwgiMo,enr:-LK4QPKVZ17v0LLrgqAABIIGTfcsBBdJWJhdVAP1AYFDzsR-R2JMNa8hoDzL69lXnBvzJFZ_wz6pOUCVtLcXol23R-UEh2F0dG5ldHOIAADAAAAAAACEZXRoMpCvgSqQYEWHOQIAAAAAAAAAgmlkgnY0gmlwhJ3ma_eJc2VjcDI1NmsxoQOTgCD2MKWSQ1TC6YSqfb4G_YjShuBN30wxfxnSKFO0QoN0Y3CCIyiDdWRwgiMo,enr:-LK4QFYBXs6DzYHc7plevcKEtNZg8AphgTIZvxBQqzilTJFgGOP2yyjsCzXhF0hV2B4y9r5TYg0PmhPVKwbfeXchDCMEh2F0dG5ldHOIBgAAAAAAAACEZXRoMpCvgSqQYEWHOQIAAAAAAAAAgmlkgnY0gmlwhC5l1wqJc2VjcDI1NmsxoQIAZ02UUtFj9Z3JH0Akc8xj67cQNVHKerP1rn5810KMHoN0Y3CCIyiDdWRwgiMo,enr:-LK4QCoLOVLB_mXCovg_rDu0brlWXx-cob4hbbuzBv5uRH4efNBU6yC-Z0Ei_J3rvtU6wteGpiQfp60oZTD5v_oDbggEh2F0dG5ldHOIYAAAAAAAAACEZXRoMpCvgSqQYEWHOQIAAAAAAAAAgmlkgnY0gmlwhEDiXo6Jc2VjcDI1NmsxoQJqGVKWLLNaAaPLvws34f-NGIEKRF-hpVPayQrGVQkCF4N0Y3CCIyiDdWRwgiMo" \
    --http \
    --http-allow-origin '*'
  ```

> Note: the bootnodes are taken from [here](https://github.com/ethpandaops/pectra-devnets/blob/master/network-configs/devnet-2/metadata/bootstrap_nodes.txt)

## Run Otterscan

- Run the development build of Otterscan.
  ```shell
  docker run \
    --rm \
    --name otterscan-pectra-devnet-2 \
    --pull always \
    -p 3100:80 \
    --env ERIGON_URL="http://localhost:8545" \
    --env BEACON_API_URL="http://localhost:5052" \
    otterscan/otterscan:develop
  ```
- Point your browser to <http://localhost:3100>