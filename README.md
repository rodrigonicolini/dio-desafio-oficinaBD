
# 🧰 Sistema de Gerenciamento de Oficina Mecânica

Este projeto tem como objetivo modelar e implementar um banco de dados relacional para o contexto de uma **oficina mecânica**, abrangendo clientes, veículos, ordens de serviço, peças e serviços prestados.  
Inclui o **modelo conceitual (ER)**, **modelo lógico**, **script SQL de criação** e **consultas SQL demonstrativas**.

---

## 📘 Estrutura do Projeto

```
📂 oficina-mecanica-bd
├── 📄 README.md
├── 📄 modelo_ER.png
├── 📄 modelo_logico.sql
└── 📄 consultas_exemplo.sql
```

---

## 🧩 Modelo Conceitual (ER)

O **modelo entidade-relacionamento (ER)** define as principais entidades do sistema:

- **Cliente** → informações de clientes da oficina  
- **Veículo** → dados dos veículos atendidos  
- **Serviço** → serviços disponíveis  
- **Peça** → peças utilizadas nas manutenções  
- **Ordem de Serviço** → registro de atendimentos  
- **Item_Serviço** → relação entre serviços e ordens  
- **Item_Peça** → relação entre peças e ordens  

📊 O diagrama ER está disponível no arquivo `modelo_ER.png`.

---

## 🗄️ Modelo Lógico e Script SQL

O script de criação (`modelo_logico.sql`) contém:

- Criação do **banco de dados** `Oficina`
- Definição das **tabelas** com chaves primárias e estrangeiras  
- Implementação dos **relacionamentos** entre entidades  

Exemplo de criação de tabela:

```sql
CREATE TABLE Cliente (
    id_cliente INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    telefone VARCHAR(20),
    email VARCHAR(100),
    endereco VARCHAR(150)
);
```

---

## 🔍 Consultas SQL (Exemplos)

O arquivo `consultas_exemplo.sql` contém exemplos de consultas, incluindo:

### 1. Recuperação simples
```sql
SELECT nome, telefone, email FROM Cliente;
```

### 2. Filtros com WHERE
```sql
SELECT * FROM Veiculo WHERE marca = 'Toyota' AND ano >= 2020;
```

### 3. Atributo derivado (valor total de OS)
```sql
SELECT os.id_os, 
       SUM(iserv.valor_total + ipec.valor_total) AS valor_total_os
FROM Ordem_Servico os
LEFT JOIN Item_Servico iserv ON os.id_os = iserv.id_os
LEFT JOIN Item_Peca ipec ON os.id_os = ipec.id_os
GROUP BY os.id_os;
```

### 4. Ordenação com ORDER BY
```sql
SELECT nome FROM Cliente ORDER BY nome ASC;
```

### 5. Filtros em grupos com HAVING
```sql
SELECT c.nome, COUNT(v.id_veiculo) AS qtd_veiculos
FROM Cliente c
JOIN Veiculo v ON c.id_cliente = v.id_cliente
GROUP BY c.nome
HAVING COUNT(v.id_veiculo) > 2;
```

---

## 🧑‍💻 Tecnologias Utilizadas

- **MySQL / MariaDB**
- **SQL ANSI**
- **Diagrama ER** (modelado visualmente)
- **Git & GitHub** para versionamento

---

## 🚀 Como Utilizar

1. Clone este repositório:
   ```bash
   git clone https://github.com/seu-usuario/oficina-mecanica-bd.git
   ```
2. Acesse o diretório:
   ```bash
   cd oficina-mecanica-bd
   ```
3. Execute o script SQL no seu banco:
   ```bash
   mysql -u root -p < modelo_logico.sql
   ```
4. Teste as consultas:
   ```bash
   mysql -u root -p < consultas_exemplo.sql
   ```

---

## 📄 Licença

Este projeto é de uso **educacional** e está sob a licença **MIT**.  
Sinta-se à vontade para copiar, modificar e usar para fins acadêmicos.

---

## ✍️ Autor

**Rodrigo**  
📧 Contato: *[seu-email@exemplo.com]*  
📍 Projeto acadêmico de modelagem de banco de dados.
