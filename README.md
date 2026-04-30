# 📊 Pipeline de Dados com IoT e Docker

## 📌 Sobre o Projeto

Este projeto tem como objetivo construir um pipeline de dados completo utilizando tecnologias modernas como IoT, Docker, PostgreSQL e Python.

A ideia central é simular um cenário real onde dispositivos IoT geram dados continuamente — neste caso, leituras de temperatura — e esses dados precisam ser processados, armazenados e visualizados de forma eficiente.

Ao longo do desenvolvimento, foi possível trabalhar conceitos importantes de engenharia de dados, como ingestão, transformação e visualização de dados.

---

## 🚀 Tecnologias Utilizadas

* **Python** → processamento e manipulação de dados
* **Docker** → containerização do banco de dados
* **PostgreSQL** → armazenamento estruturado
* **Pandas / SQLAlchemy** → integração entre aplicação e banco
* **Streamlit** → criação do dashboard
* **Plotly** → visualizações interativas

---

## 📁 Estrutura do Projeto

```
📦 pipeline-iot
 ┣ 📂 data
 ┃ ┗ 📄 temperature_readings.csv
 ┣ 📂 src
 ┃ ┣ 📄 main.py
 ┃ ┗ 📄 dashboard.py
 ┣ 📂 sql
 ┃ ┗ 📄 views.sql
 ┣ 📄 requirements.txt
 ┣ 📄 README.md
```

---

## ⚙️ Como Executar o Projeto

### 1. Clonar o repositório

```bash
git clone https://github.com/seu-usuario/seu-repositorio.git
cd seu-repositorio
```

---

### 2. Criar ambiente virtual

```bash
python -m venv venv
```

Ativar o ambiente:

* Windows:

```bash
venv\Scripts\activate
```

* Linux/Mac:

```bash
source venv/bin/activate
```

---

### 3. Instalar dependências

```bash
pip install -r requirements.txt
```

---

### 4. Subir o PostgreSQL com Docker

```bash
docker run --name postgres-iot \
-e POSTGRES_PASSWORD=123456 \
-p 5432:5432 \
-d postgres
```

---

### 5. Configurar conexão com o banco

No código Python, ajuste a string de conexão:

```python
postgresql://postgres:123456@localhost:5432/postgres
```

---

### 6. Executar o processamento dos dados

```bash
python src/main.py
```

Esse script irá:

* Ler o arquivo CSV
* Processar os dados
* Inserir no PostgreSQL

---

### 7. Criar as Views SQL

Execute o script:

```sql
CREATE VIEW avg_temp_por_dispositivo AS
SELECT device_id, AVG(temperature) AS avg_temp
FROM temperature_readings
GROUP BY device_id;

CREATE VIEW leituras_por_hora AS
SELECT EXTRACT(HOUR FROM timestamp) AS hora, COUNT(*) AS contagem
FROM temperature_readings
GROUP BY hora;

CREATE VIEW temp_max_min_por_dia AS
SELECT DATE(timestamp) AS data,
       MAX(temperature) AS temp_max,
       MIN(temperature) AS temp_min
FROM temperature_readings
GROUP BY data;
```

---

### 8. Executar o dashboard

```bash
streamlit run src/dashboard.py
```

Depois disso, o dashboard estará disponível no navegador.

---

## 📊 Dashboard

O dashboard apresenta três análises principais:

* 📈 Média de temperatura por dispositivo
* ⏱️ Volume de leituras por hora
* 🌡️ Temperaturas máximas e mínimas por dia

As visualizações são interativas e permitem uma análise mais intuitiva dos dados.

---

## 💡 Insights Obtidos

Durante a análise dos dados, foi possível observar:

* Diferença de comportamento entre dispositivos
* Picos de leitura em determinados horários
* Variações de temperatura que podem indicar anomalias

Esses insights poderiam ser utilizados, por exemplo, para manutenção preventiva ou monitoramento em tempo real.

---

## 🧠 Aprendizados

Este projeto permitiu colocar em prática conceitos importantes como:

* Construção de pipeline de dados
* Integração entre sistemas
* Uso de containers com Docker
* Visualização de dados de forma eficiente

Além disso, mostrou como diferentes tecnologias podem trabalhar juntas para resolver um problema real.

---

## 📦 Base de Dados

Dataset utilizado:
Temperature Readings: IoT Devices (Kaggle)

---

## 👨‍💻 Autor

Projeto desenvolvido como parte da disciplina **Disruptive Architectures: IoT, Big Data e IA**.

---

## 📌 Observações

* Certifique-se de que o Docker esteja rodando
* Verifique se a porta 5432 não está sendo utilizada
* Ajuste credenciais conforme necessário

---

💬 Se quiser contribuir ou melhorar o projeto, fique à vontade!
