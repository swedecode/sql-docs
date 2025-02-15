---
description: "ENCRYPTBYCERT (Transact-SQL)"
title: "ENCRYPTBYCERT (Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: sql
ms.prod_service: "database-engine, sql-database"
ms.reviewer: ""
ms.technology: t-sql
ms.topic: reference
f1_keywords: 
  - "ENCRYPTBYCERT"
  - "ENCRYPTBYCERT_TSQL"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "certificates [SQL Server], encryption"
  - "encryption [SQL Server], certificates"
  - "ENCRYPTBYCERT function"
ms.assetid: ab66441f-e2d2-4e3a-bcae-bcc09e12f3c1
author: VanMSFT
ms.author: vanto
---
# ENCRYPTBYCERT (Transact-SQL)
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

Encrypts data with the public key of a certificate.  
  
![Topic link icon](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```syntaxsql
EncryptByCert ( certificate_ID , { 'cleartext' | @cleartext } )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments
_certificate\_ID_  
The ID of a certificate in the database. **int**.  
  
_cleartext_  
A string of data that will be encrypted with the certificate.  
  
**\@cleartext**  
A variable of one of the following types that contains data that will be encrypted with the public key of the certificate:

* **nvarchar** 
* **char**
* **varchar**
* **binary** 
* **varbinary**
* **nchar**
  
## Return Types  
**varbinary** with a maximum size of 8,000 bytes.  
  
## Remarks  
This function encrypts data with the certificate's public key. The ciphertext can only be decrypted with the corresponding private key. These asymmetric transformations are costly when compared to encryption and decryption using a symmetric key. As such, asymmetric encryption isn't recommended when working with large datasets.
  
## Examples  
This example encrypts the plaintext stored in `@cleartext` with the certificate called `JanainaCert02`. The encrypted data is inserted into table `ProtectedData04`.  
  
```sql  
INSERT INTO [AdventureWorks2012].[ProtectedData04]   
    VALUES ( N'Data encrypted by certificate ''Shipping04''',  
    EncryptByCert(Cert_ID('JanainaCert02'), @cleartext) );  
GO  
```  
  
## See Also  
[DECRYPTBYCERT &#40;Transact-SQL&#41;](../../t-sql/functions/decryptbycert-transact-sql.md)   
[CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
[ALTER CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
[DROP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
[BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
[Encryption Hierarchy](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
