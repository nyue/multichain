CMAKE_MINIMUM_REQUIRED ( VERSION 2.8 )

PROJECT ( MultiChain )

FIND_PACKAGE ( Boost REQUIRED COMPONENTS system thread program_options filesystem )
FIND_PACKAGE ( Threads REQUIRED )
FIND_PACKAGE ( OpenSSL REQUIRED )

INCLUDE_DIRECTORIES ( ${Boost_INCLUDE_DIR} )

ADD_SUBDIRECTORY ( src )

