# SM1分组密码

SM1分组密码和SSF33分组密码均为国密分组密码标标准，SM1和SSF33的密钥长度和分组长度均为128比特。

目前这两个分组密码标准的算法尚未公开，其实现仅可以通过硬件芯片的方式获得，目前很多国产密码设备均包含这两个分组密码的硬件实现，由国家密码管理局制定的《智能IC卡及智能密码钥匙密码应用接口规范》中包含了对SM1分组密码的ECB、CBC、CFB、OFB加密模式和CBC-MAC的算法定义。

GmSSL提供了SM1和SSF33分组密码各种工作模式的定义，但并未包含其软件实现。在调用SM1或SSF33的功能时，需要接入支持相应算法的硬件密码设备。GmSSL通过内置的ENGINE访问支持《智能IC卡及智能密码钥匙密码应用接口规范》的密码硬件，因此原则上可以支持所有提供该接口的国密硬件。

## 通过ENGINE调用SM1分组密码

```c
/* load engine with SM1 support */
ENGINE *engine = ENGINE_by_id("sdf");
if (engine == NULL) goto err;

/* load sm1-cbc cipher from engine */
const EVP_CIPHER *cipher = ENGINE_get_cipher(engine, NID_sm1_cbc);
if (cipher == NULL) goto err;

/* encrypt with sm1-cbc implemented with engine */
EVP_CIPHER_CTX *cctx = EVP_CIPHER_CTX_new();
if (cctx == NULL) goto err;
if (1 != EVP_EncryptInit_ex(cctx, cipher, engine, key, iv)) goto err;
if (1 != EVP_EncryptUpdate(cctx, ...)) goto err;
if (1 != EVP_EncryptFinal_ex(cctx, ...)) goto err;
```

## SM1测试数据：

### SM1-ECB

```c
unsigned char key[16] = {
	0x40,0xbb,0x12,0xdd,0x6a,0x82,0x73,0x86,0x7f,0x35,0x29,0xd3,0x54,0xb4,0xa0,0x26
};
unsigned char plaintext[16] = {
	0xff,0xee,0xdd,0xcc,0xbb,0xaa,0x99,0x88,0x77,0x66,0x55,0x44,0x33,0x22,0x11,0x00
};
unsigned char ciphertext[16] = {
	0x6d,0x7f,0x45,0xb0,0x8b,0xc4,0xd9,0x66,0x44,0x4c,0x86,0xc2,0xb0,0x7d,0x29,0x93};
```

### SM1-CBC

```c
unsigned char sm1_cbc_test_key[16] = {
	0x40,0xbb,0x12,0xdd,0x6a,0x82,0x73,0x86,0x7f,0x35,0x29,0xd3,0x54,0xb4,0xa0,0x26
};
unsigned char sm1_cbc_test_iv[16] = {
	0xe8,0x3d,0x17,0x15,0xac,0xf3,0x48,0x63,0xac,0xeb,0x93,0xe0,0xe5,0xab,0x8b,0x90
};
unsigned char sm1_cbc_test_plaintext[32] = {
	0xff,0xee,0xdd,0xcc,0xbb,0xaa,0x99,0x88,0x77,0x66,0x55,0x44,0x33,0x22,0x11,0x00,
	0x00,0x11,0x22,0x33,0x44,0x55,0x66,0x77,0x88,0x99,0xaa,0xbb,0xcc,0xdd,0xee,0xff
};
unsigned char sm1_cbc_test_ciphertext[32] = {
	0x3a,0x70,0xb5,0xd4,0x9a,0x78,0x2c,0x07,0x2d,0xe1,0x13,0x43,0x81,0x9e,0xc6,0x59,
	0xf8,0xfc,0x7a,0xf0,0x5e,0x7c,0x6d,0xfb,0x5f,0x81,0x09,0x0f,0x0d,0x87,0x91,0xb2};
```
