INCLUDE_DIRECTORIES ( . )
INCLUDE_DIRECTORIES ( ./secp256k1/include )
INCLUDE_DIRECTORIES ( ./leveldb/include )
INCLUDE_DIRECTORIES ( ./leveldb/helpers/memenv )

ADD_SUBDIRECTORY ( leveldb )

IF (NOT WIN32)
  ADD_DEFINITIONS ( -DHAVE_SYS_SELECT_H -DHAVE_DECL_STRNLEN -DHAVE_WORKING_BOOST_SLEEP_FOR -DENABLE_WALLET )
ENDIF ()

ADD_LIBRARY ( bitcoinconcensus
  primitives/transaction.cpp
  crypto/hmac_sha512.cpp
  crypto/sha1.cpp
  crypto/sha256.cpp
  crypto/sha512.cpp
  crypto/ripemd160.cpp
  utils/utility.cpp
  utils/systemdependent.cpp
  utils/tools.cpp
  utils/utilwrapper.cpp
  chainparams/buildgenesis.cpp
  version/version.cpp
  chainparams/chainparams.cpp
  protocol/multichainscript.cpp
  utils/dbwrapper.cpp
  wallet/wallettxdb.cpp
  permissions/permission.cpp
  entities/asset.cpp
  structs/hash.cpp
  keys/pubkey.cpp
  script/script.cpp
  script/interpreter.cpp
  script/bitcoinconsensus.cpp
  structs/uint256.cpp
  utils/utilstrencodings.cpp
  compat/glibc_compat.cpp
  compat/glibcxx_compat.cpp
)

ADD_LIBRARY ( bitcoin_common
  utils/allocators.cpp
  structs/amount.cpp
  structs/base58.cpp
  chainparams/chainparams.cpp
  storage/coins.cpp
  utils/compressor.cpp
  primitives/block.cpp
  primitives/transaction.cpp
  utils/core_read.cpp
  utils/core_write.cpp
  structs/hash.cpp
  keys/key.cpp
  wallet/keystore.cpp
  net/netbase.cpp
  protocol/netprotocol.cpp
  keys/pubkey.cpp
  script/interpreter.cpp
  script/script.cpp
  script/sign.cpp
  script/standard.cpp
  script/script_error.cpp
)

ADD_LIBRARY ( bitcoin_util
  compat/strnlen.cpp
  compat/glibc_sanity.cpp
  compat/glibcxx_sanity.cpp
  chainparams/chainparamsbase.cpp
  version/clientversion.cpp
  utils/random.cpp
  rpc/rpcprotocol.cpp
  utils/sync.cpp
  structs/uint256.cpp
  utils/util.cpp
  utils/utilstrencodings.cpp
  utils/utilmoneystr.cpp
  utils/utiltime.cpp
  compat/glibc_compat.cpp
  compat/glibcxx_compat.cpp
  )

ADD_LIBRARY ( bitcoin_cli
  rpc/rpcclient.cpp
  )

ADD_LIBRARY ( bitcoin_crypto
  crypto/sha1.cpp
  crypto/sha256.cpp
  crypto/sha512.cpp
  crypto/hmac_sha256.cpp
  crypto/hmac_sha512.cpp
  crypto/ripemd160.cpp

  )

ADD_LIBRARY ( bitcoin_multichain
utils/utility.cpp
  utils/systemdependent.cpp
  utils/tools.cpp
  utils/utilwrapper.cpp
  version/version.cpp
  chainparams/params.cpp
  protocol/multichainscript.cpp
  utils/dbwrapper.cpp
  wallet/wallettxdb.cpp
  permissions/permission.cpp
  entities/asset.cpp
  )

ADD_LIBRARY ( bitcoin_univalue
  univalue/univalue.cpp
  univalue/univalue_read.cpp
  univalue/univalue_write.cpp
  )

ADD_LIBRARY ( multichain_util
  multichain/multichain-util.cpp
  chainparams/buildgenesis.cpp
  )

ADD_EXECUTABLE ( multichaind
  multichain/multichaind.cpp
  chainparams/buildgenesis.cpp
  )

SET ( REQUIRED_LINK_LIBRARIES
  bitcoin_cli
  bitcoin_util
  bitcoinconcensus
  bitcoin_multichain
  bitcoin_univalue
  bitcoin_crypto
  bitcoin_common
  db
  memenv
  ${Boost_LIBRARIES}
  ${CMAKE_THREAD_LIBS_INIT}
  ${OPENSSL_CRYPTO_LIBRARY}
  ${OPENSSL_SSL_LIBRARY}
  )

TARGET_LINK_LIBRARIES ( multichaind
  ${REQUIRED_LINK_LIBRARIES}
  )

ADD_EXECUTABLE ( multichain_cli
  multichain/multichain-cli.cpp
  )

TARGET_LINK_LIBRARIES ( multichain_cli
  ${REQUIRED_LINK_LIBRARIES}
  )

ADD_EXECUTABLE ( bitcoin_server
  storage/addrman.cpp
  structs/alert.cpp
  structs/bloom.cpp
  chain/chain.cpp
  chain/checkpoints.cpp
  core/init.cpp
  storage/leveldbwrapper.cpp
  core/main.cpp
  protocol/multichaintx.cpp
  protocol/multichainblock.cpp
  protocol/handshake.cpp
  chain/merkleblock.cpp
  miner/miner.cpp
  net/net.cpp
  ui/noui.cpp
  chain/pow.cpp
  net/rest.cpp
  utils/utilparse.cpp
  rpc/rpcutils.cpp
  rpc/rpchelp.cpp
  rpc/rpcblockchain.cpp
  rpc/rpcmining.cpp
  rpc/rpcmisc.cpp
  rpc/rpcnet.cpp
  rpc/rpcrawtransaction.cpp
  rpc/rpcserver.cpp
  script/sigcache.cpp
  utils/timedata.cpp
  storage/txdb.cpp
  chain/txmempool.cpp
  )

TARGET_LINK_LIBRARIES ( bitcoin_server
  ${REQUIRED_LINK_LIBRARIES}
  )
