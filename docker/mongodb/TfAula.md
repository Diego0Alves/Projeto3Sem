# TF da Aula de Banco de Dados do dia: 23/04/2025

## Consulta de dados

### 1. Encontrando clientes em São Paulo.

```sh

db.client.find({ city: "São Paulo" });

```

### 2. Encontrando processos com valor maior que 2000.

```sh

db.client_processes.find({ value: { $gt: 2000 } });

```

### 3. Encontrando eventos com proposta pendente ou aceita.

```sh

db.events.find({ proposal_status: { $in: ["pending accepted", "accepted"] } });

```

### 4. Encontrando clientes em que o campo "enterprise" não é "null".

```sh

db.client.find(
  { enterprise: { $ne: null } },
  { full_name: 1, cnpj_enterprise: 1, _id: 0 }
);

```

### 5. Encontrando todos processos de classe "Cobrança" e ordenando em ordem decrescente.

```sh

db.client_processes.find({ class: "Cobrança" }).sort({ value: -1 });

```

## Atualizando dados

### 1. Alterando status do processo com "number: PROC-2023-001" para "concluído".

```sh

db.client_processes.updateOne(
  { number: "PROC-2023-001" },
  { $set: { status: "concluído" } }
);

```

### 2. Adiciona o campo "note_doc" com o valor "OBS-MS-001.txt" ao evento de Maria Silva.

```sh

db.events.updateOne(
  { client_id: "id_do_cliente_maria_silva" },
  { $set: { note_doc: "OBS-MS-001.txt" } }
);

```

### 3. Aumenta em 1 a "amount_of_cleaning" para o evento da Empresa Soluções Ltda.

```sh

db.events.updateOne(
  { client_id: "id_do_cliente_empresa_solucoes" },
  { $inc: { amount_of_cleaning: 1 } }
);

```

## Excluindo dados

### 1. Removendo o processo com number "PROC-2023-002".

```sh

db.client_processes.deleteOne({ number: "PROC-2023-002" });

```

### 2. Removendo clientes com o campo "cnpj_enterprise é null".

```sh

db.client.deleteMany({ cnpj_enterprise: null });

```

## Criando índices

### 1. Cria um índice no campo full_name da coleção client.

```sh

db.client.createIndex({ full_name: 1 });

```

### 2. Lista todos os índices da coleção client.

```sh

db.client.getIndexes();

```