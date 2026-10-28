# Программный код ИС

## 1. Структура базы данных (SQL)
Для хранения информации о договорах спроектирована реляционная база данных. Ниже приведен скрипт создания основной таблицы:

CREATE TABLE Contracts (
    ContractID INT PRIMARY KEY AUTO_INCREMENT,
    ContractNumber VARCHAR(50) NOT NULL,
    SigningDate DATE,
    Counterparty VARCHAR(255) NOT NULL,
    Amount DECIMAL(15, 2),
    Status ENUM('Active', 'Completed', 'Expired')
);

## 2. Псевдокод логики контроля сроков (Python)
Логика ежедневной проверки сроков может быть реализована следующим образом:

def check_contract_deadlines():
    active_contracts = database.get_active_contracts()
    for contract in active_contracts:
        days_left = (contract.end_date - today).days
        if days_left <= 3:
            send_notification(contract.manager_email, contract.number)