
Open DID TAS Database Table Definition
==

- Date: 2024-09-04
- Version: v1.0.0

Contents
--
- [1. Overview](#1-overview)
- [2. Table Definition](#2-table-definition)
    - [2.1. TAS](#21-tas)
    - [2.2. ENTITY](#22-entity)
    - [2.3. USER](#23-user)
    - [2.4. WALLET](#24-wallet)
    - [2.5. APP](#25-app)
    - [2.6. CERTIFICATE_VC](#26-certificate_vc)
    - [2.7. TRANSACTION](#27-transaction)
    - [2.8. SUB_TRANSACTION](#28-sub_transaction)
    - [2.9. TOKEN](#29-token)
    - [2.10. ECDH](#210-ecdh)
    - [2.11. DID_OFFER](#211-did_offer)

## 1. Overview

This document defines the structure of the database tables used in the TAS server. It describes the field attributes, relationships, and data flow for each table, serving as essential reference material for system development and maintenance.

### 1.1 ERD

Access the [ERD](https://www.erdcloud.com/d/ypN72iPhhA4F46FSd) site to view the diagram, which visually represents the relationships between the tables in the TAS server database, including key attributes, primary keys, and foreign key relationships.

## 2. Table Definition

### 2.1. TAS

This table stores information related to TAS.

| Key  | Column Name        | Data Type  | Length | Nullable | Default  | Description                       |
|------|--------------------|------------|--------|----------|----------|-----------------------------------|
| PK   | id                 | BIGINT     |        | NO       | N/A      | id                                |
|      | did                | VARCHAR    | 200    | NO       | N/A      | tas did                           |
|      | name               | VARCHAR    | 200    | NO       | N/A      | tas name                          |
|      | status             | VARCHAR    | 50     | NO       | N/A      | tas status                        |
|      | server_url         | VARCHAR    | 2000   | NO       | N/A      | tas server URL                    |
|      | certificate_url    | VARCHAR    | 2000   | YES      | N/A      | tas's certificate VC URL          |
|      | created_at         | TIMESTAMP  |        | NO       | now()    | created date                      |
|      | updated_at         | TIMESTAMP  |        | YES      | N/A      | updated date                      |

---


### 2.2. ENTITY

This table stores information related to entities.

| Key  | Column Name        | Data Type  | Length | Nullable | Default  | Description                       |
|------|--------------------|------------|--------|----------|----------|-----------------------------------|
| PK   | id                 | BIGINT     |        | NO       | N/A      | entity id                         |
|      | did                | VARCHAR    | 200    | NO       | N/A      | entity did                        |
|      | name               | VARCHAR    | 200    | NO       | N/A      | entity name                       |
|      | role               | VARCHAR    | 30     | NO       | N/A      | entity role                       |
|      | status             | VARCHAR    | 50     | NO       | N/A      | entity status                     |
|      | server_url         | VARCHAR    | 2000   | NO       | N/A      | entity server URL                 |
|      | certificate_url    | VARCHAR    | 2000   | YES      | N/A      | entity's certificate VC URL       |
|      | created_at         | TIMESTAMP  |        | NO       | now()    | created date                      |
|      | updated_at         | TIMESTAMP  |        | YES      | N/A      | updated date                      |


### 2.3. USER

This table stores information related to users.

| Key  | Column Name        | Data Type  | Length | Nullable | Default  | Description                       |
|------|--------------------|------------|--------|----------|----------|-----------------------------------|
| PK   | id                 | BIGINT     |        | NO       | N/A      | id                                |
|      | did                | VARCHAR    | 200    | NO       | N/A      | user did                          |
|      | status             | VARCHAR    | 50     | NO       | N/A      | user status                       |
|      | pii                | VARCHAR    | 100    | NO       | N/A      | user pii                          |
|      | created_at         | TIMESTAMP  |        | NO       | now()    | created date                      |
|      | updated_at         | TIMESTAMP  |        | YES      | N/A      | updated date                      |


### 2.4. WALLET

This table stores information related to wallets.

| Key  | Column Name        | Data Type  | Length | Nullable | Default  | Description                       |
|------|--------------------|------------|--------|----------|----------|-----------------------------------|
| PK   | id                 | BIGINT     |        | NO       | N/A      | id                                |
|      | wallet_id          | VARCHAR    | 200    | NO       | N/A      | wallet ID                         |
|      | did                | VARCHAR    | 200    | NO       | N/A      | wallet did                        |
|      | status             | VARCHAR    | 50     | NO       | N/A      | wallet status                     |
|      | registered_at      | TIMESTAMP  |        | NO       | N/A      | wallet registration date          |
|      | cancelled_at       | TIMESTAMP  |        | YES      | N/A      | wallet termination date           |
|      | created_at         | TIMESTAMP  |        | NO       | now()    | created date                      |
|      | updated_at         | TIMESTAMP  |        | YES      | N/A      | updated date                      |
|      | user_id            | BIGINT     |        | YES      | N/A      | user table key                    |
|      | entity_id          | BIGINT     |        | NO       | N/A      | entity table key                  |


### 2.5. APP

This table stores information related to apps.

| Key  | Column Name        | Data Type  | Length | Nullable | Default  | Description                       |
|------|--------------------|------------|--------|----------|----------|-----------------------------------|
| PK   | id                 | BIGINT     |        | NO       | N/A      | entity table key                  |
|      | app_id             | VARCHAR    | 20     | NO       | N/A      | app ID                            |
|      | push_token         | VARCHAR    | 255    | YES      | N/A      | push token                        |
|      | status             | VARCHAR    | 50     | NO       | N/A      | app status                        |
|      | created_at         | TIMESTAMP  |        | NO       | now()    | created date                      |
|      | updated_at         | TIMESTAMP  |        | YES      | N/A      | updated date                      |
|      | user_id            | BIGINT     |        | NO       | N/A      | user table key                    |


### 2.6. CERTIFICATE_VC

This table stores information related to certificate VCs.

| Key  | Column Name        | Data Type  | Length | Nullable | Default  | Description                                |
|------|--------------------|------------|--------|----------|----------|--------------------------------------------|
| PK   | id                 | BIGINT     |        | NO       | N/A      | id                                         |
|      | vc                 | TEXT       |        | NO       | N/A      | certificate VC contents (json)             |
|      | created_at         | TIMESTAMP  |        | NO       | now()    | created date                               |
|      | updated_at         | TIMESTAMP  |        | YES      | N/A      | updated date                               |


### 2.7. TRANSACTION

This table stores information related to transactions.

| Key  | Column Name        | Data Type  | Length | Nullable | Default  | Description                                |
|------|--------------------|------------|--------|----------|----------|--------------------------------------------|
| PK   | id                 | BIGINT     |        | NO       | N/A      | id                                         |
|      | tx_id              | VARCHAR    | 40     | NO       | N/A      | transaction id                             |
|      | type               | VARCHAR    | 50     | NO       | N/A      | transaction type                           |
|      | status             | VARCHAR    | 50     | NO       | N/A      | transaction status                         |
|      | did                | VARCHAR    | 200    | YES      | N/A      | transaction target did                     |
|      | auth_nonce         | VARCHAR    | 100    | YES      | N/A      | DID Auth nonce                             |
|      | certificate_id     | VARCHAR    | 50     | YES      | N/A      | certificate VC ID                          |
|      | external_tx_id     | VARCHAR    | 40     | YES      | N/A      | external server transaction id             |
|      | external_did       | VARCHAR    | 200    | YES      | N/A      | external server did                        |
|      | pii                | VARCHAR    | 100    | YES      | N/A      | user pii                                   |
|      | expired_at         | TIMESTAMP  |        | NO       | N/A      | expiration date                            |
|      | created_at         | TIMESTAMP  |        | NO       | now()    | created date                               |
|      | updated_at         | TIMESTAMP  |        | YES      | N/A      | updated date                               |


### 2.8. SUB_TRANSACTION

This table stores information related to sub-transactions.

| Key  | Column Name        | Data Type  | Length | Nullable | Default  | Description                                |
|------|--------------------|------------|--------|----------|----------|--------------------------------------------|
| PK   | id                 | BIGINT     |        | NO       | N/A      | id                                         |
|      | step               | SMALLINT   |        | NO       | N/A      | sub transaction step                       |
|      | type               | VARCHAR    | 50     | NO       | N/A      | sub transaction type                       |
|      | status             | VARCHAR    | 50     | NO       | N/A      | sub transaction status                     |
|      | created_at         | TIMESTAMP  |        | NO       | now()    | created date                               |
|      | updated_at         | TIMESTAMP  |        | YES      | N/A      | updated date                               |
|      | transaction_id     | BIGINT     |        | NO       | N/A      | transaction table key                      |


### 2.9. TOKEN

This table stores information related to tokens.

| Key  | Column Name        | Data Type  | Length | Nullable | Default  | Description                                |
|------|--------------------|------------|--------|----------|----------|--------------------------------------------|
| PK   | id                 | BIGINT     |        | NO       | N/A      | id                                         |
|      | purpose            | VARCHAR    | 50     | NO       | N/A      | token purpose                              |
|      | token              | VARCHAR    | 200    | NO       | N/A      | token                                      |
|      | app_id             | VARCHAR    | 20     | NO       | N/A      | app id                                     |
|      | wallet_id          | VARCHAR    | 200    | NO       | N/A      | wallet id                                  |
|      | expired_at         | TIMESTAMP  |        | NO       | N/A      | expiration date                            |
|      | created_at         | TIMESTAMP  |        | NO       | now()    | created date                               |
|      | updated_at         | TIMESTAMP  |        | YES      | N/A      | updated date                               |
|      | transaction_id     | BIGINT     |        | NO       | N/A      | transaction management table key           |


### 2.10. ECDH

This table stores information related to ECDH transactions.

| Key  | Column Name        | Data Type  | Length | Nullable | Default  | Description                                |
|------|--------------------|------------|--------|----------|----------|--------------------------------------------|
| PK   | id                 | BIGINT     |        | NO       | N/A      | id                                         |
|      | client_did         | VARCHAR    | 200    | NO       | N/A      | client did                                 |
|      | session_key        | VARCHAR    | 100    | NO       | N/A      | session key                                |
|      | nonce              | VARCHAR    | 100    | NO       | N/A      | nonce                                      |
|      | cipher             | VARCHAR    | 20     | NO       | N/A      | cipher type                                |
|      | padding            | VARCHAR    | 20     | NO       | N/A      | padding type                               |
|      | created_at         | TIMESTAMP  |        | NO       | now()    | created date                               |
|      | updated_at         | TIMESTAMP  |        | YES      | N/A      | updated date                               |
|      | transaction_id     | BIGINT     |        | NO       | N/A      | transaction management table key           |


### 2.11. DID_OFFER

This table stores information related to DID offers.

| Key  | Column Name        | Data Type  | Length | Nullable | Default  | Description                                |
|------|--------------------|------------|--------|----------|----------|--------------------------------------------|
| PK   | id                 | BIGINT     |        | NO       | N/A      | id                                         |
|      | offier_id          | VARCHAR    | 40     | NO       | N/A      | did offer id                               |
|      | type               | VARCHAR    | 50     | NO       | N/A      | did offer type                             |
|      | did                | VARCHAR    | 200    | NO       | N/A      | user did                                   |
|      | valid_until        | TIMESTAMP  |        | YES      | N/A      | did offer expiration date                  |
|      | created_at         | TIMESTAMP  |        | NO       | now()    | created date                               |
|      | updated_at         | TIMESTAMP  |        | YES      | N/A      | updated date                               |
|      | transaction_id     | BIGINT     |        | YES      | N/A      | transaction management table key           |