# LAB5 – Intégration Spring & Hibernate avec MySQL

## Introduction

L'objectif de ce TP est d'intégrer **Spring Framework** avec **Hibernate** pour gérer la persistance des données via une base de données MySQL. Spring prend en charge l'injection de dépendances et la gestion des transactions, tandis qu'Hibernate assure le mapping objet-relationnel (ORM) de l'entité `Product`.

---

## Structure du Projet

```
spring-hibernate-demo/
├── src/
│   └── main/
│       ├── java/
│       │   ├── com.example/
│       │   │   └── App.java
│       │   ├── dao/
│       │   │   └── IDao.java                  # Interface générique DAO
│       │   ├── entities/
│       │   │   └── Product.java               # Entité persistante
│       │   ├── metier/
│       │   │   └── ProductDaoImpl.java        # Implémentation CRUD
│       │   ├── util/
│       │   │   └── HibernateConfig.java       # Configuration Spring + Hibernate
│       │   ├── Test.java             # Test : insertion d'un produit
│       │   └── TestHibernate.java             # Test : vérification SessionFactory
│       └── resources/
│           └── application.properties         # Paramètres MySQL & Hibernate
├── pom.xml
└── .gitignore
```

---

## Explication des Fichiers Clés

### `HibernateConfig.java`
Classe de configuration centrale de l'application. Elle joue trois rôles principaux :
- **`DataSource`** : configure la connexion MySQL (driver, URL, identifiants) à partir du fichier `application.properties` via `@Value`.
- **`SessionFactory`** : initialise Hibernate avec les propriétés (dialecte, DDL auto, affichage SQL) et indique le package à scanner pour détecter les entités.
- **`HibernateTransactionManager`** : lie la gestion des transactions Spring à la `SessionFactory` Hibernate.

### `application.properties`
Fichier de configuration externalisé contenant les paramètres de connexion MySQL et les propriétés Hibernate :

```properties
# Connexion MySQL
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasource.url=jdbc:mysql://localhost:3306/base?createDatabaseIfNotExist=true&serverTimezone=UTC
spring.datasource.username=root
spring.datasource.password=

# Hibernate
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL8Dialect
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true
```

---

## Images d'Exécution

### 1. Test `Test` – Insertion d'un produit
> Hibernate génère le `INSERT INTO Product` et confirme l'enregistrement avec **exit code 0**.

![1](https://github.com/user-attachments/assets/e2deabfa-92a1-48f6-a099-3a98446d652c)


### 2. Test `TestHibernate` – Vérification de la configuration
> La `SessionFactory` et le gestionnaire de transactions sont initialisés correctement.

![2](https://github.com/user-attachments/assets/35216b18-04dd-4551-be53-f1f5e84a4fd3)


---

## Technologies Utilisées

- Java (OpenJDK 25)
- Spring Framework 5.3.22
- Hibernate ORM 5.6.12
- MySQL 8
- Maven
- IntelliJ IDEA
