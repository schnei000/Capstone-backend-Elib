# 📚 E-Lib Backend

API REST pour gérer une bibliothèque numérique (digital library).

## 🚀 Features

- ✅ Authentification JWT
- 👥 User management (admin & users)
- 📖 Ebooks CRUD
- 🏷️ Categories
- 📅 Loan system (14 jours)
- 📧 Email notifications
- 📄 Swagger documentation

## 🛠️ Tech Stack

- **Flask** - Framework web Python
- **SQLAlchemy** - ORM database
- **JWT** - Authentication tokens
- **Bcrypt** - Password hashing
- **SQLite/PostgreSQL** - Database

## 📦 Installation

### 1. Clone le projet

```bash
git clone <url>
cd elib-backend
```

### 2. Virtual environment

```bash
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Configuration (.env file)

Créer un fichier `.env` :

```env
secret_key=ma_cle_super_secrete
jwt_secret_key=ma_cle_jwt_super_secrete
database_uri=sqlite:///bibliotheque.db
```

### 5. Initialize database

```bash
python init_db.py
```


## 🎯 Start Server

### Dev mode

```bash
python app.py
```

Server sur `http://localhost:5000`

### Production

```bash
gunicorn app:app --bind 0.0.0.0:5000
```

## 📚 API Documentation

Swagger UI : `http://localhost:5000/api/docs/`

## 🔑 Main Endpoints

### Auth
- `POST /api/users` - Register
- `POST /api/login` - Login (get JWT token)

### Users
- `GET /api/users` - List users (Admin only)
- `GET /api/users/me` - Mon profil
- `PUT /api/users/<id>` - Update user
- `DELETE /api/users/<id>` - Delete user

### Ebooks
- `GET /api/ebooks` - List books
- `GET /api/ebooks/<id>` - Book details
- `POST /api/ebooks` - Create book (Admin)
- `PUT /api/ebooks/<id>` - Update book (Admin)
- `DELETE /api/ebooks/<id>` - Delete book (Admin)

### Categories
- `GET /api/categories` - List categories
- `POST /api/categories` - Create category (Admin)
- `PUT /api/categories/<id>` - Update category (Admin)
- `DELETE /api/categories/<id>` - Delete category (Admin)

### Loans
- `GET /api/loans` - Mes emprunts
- `POST /api/loans` - Emprunter un livre
- `PUT /api/loans/<id>` - Return book
- `GET /api/users/<id>/loans` - User loans

## 🔐 Authentication

Ajouter le header pour protected routes :

```bash
Authorization: Bearer <votre_token>
```

Exemple :
```bash
curl -H "Authorization: Bearer eyJ0eXAi..." http://localhost:5000/api/users/me
```

## 🧪 Tests

```bash
# All tests
python run_tests.py

# Unit tests only
python test_backend.py

# API tests
python test_api_endpoints.py
```

## 📁 Structure

```
elib-backend/
├── app.py                   
├── config.py                
├── models.py                
├── requirements.txt         
├── .env                     
│
├── routes/                  # API routes
│   ├── route_user.py
│   ├── routes_ebook.py
│   ├── route_category.py
│   └── route_loan.py
│
└── utils/                   
    ├── email_service.py
    └── check_expired_loans.py
```

## 🌐 Deploy sur Render

### Setup Render

1. **Créer un nouveau Web Service**
   - Aller sur [render.com](https://render.com)
   - Connect ton repo GitHub
   - Choisir "Web Service"

2. **Configuration**
   ```
   Name: elib-backend
   Environment: Python 3
   Build Command: pip install -r requirements.txt
   Start Command: gunicorn app:app
   ```

3. **Add PostgreSQL Database**
   - Dans Dashboard → New → PostgreSQL
   - Copier l'Internal Database URL

4. **Environment Variables**
   ```
   secret_key=votre_cle_super_secrete
   jwt_secret_key=votre_cle_jwt_super_secrete
   database_uri=<Internal_Database_URL_de_Render>
   ```

5. **Deploy**
   - Click "Create Web Service"
   - Render va build et deploy automatiquement

6. **Init Database** 
   - Aller dans Shell tab
   ```bash
   flask db upgrade
   flask create-admin admin@elib.com Admin123
   python seed_database.py
   ```

### Auto-Deploy

Render redeploy automatiquement à chaque push sur la branche main 🚀

## 🔧 CORS Setup

Par défaut configuré pour :
- `http://localhost:5173` (Frontend local)
- `https://capstone-frontend-elib.vercel.app/` (Production)

Modifier dans `app.py` si besoin.

## 📧 Email Notifications


1. Config SMTP dans `.env`
2. Run :
```bash
python utils/check_expired_loans.py
```

## 🐛 Debug Mode

Dans `app.py` :
```python
if __name__ == '__main__':
    app.run(debug=True, port=5000)
```

## 📝 Useful Commands

```bash
# Create admin
flask create-admin email@example.com password

# Database migrations
flask db migrate -m "Description"
flask db upgrade

# Interactive shell
flask shell
```

## 💡 Quick Start Example

```bash
# 1. Install & setup
git clone <url>
cd elib-backend
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 2. Config
echo "secret_key=test123" > .env
echo "jwt_secret_key=jwt123" >> .env
echo "database_uri=sqlite:///bibliotheque.db" >> .env

# 3. Init
python init_db.py
flask create-admin admin@test.com Admin123

# 4. Run
python app.py
```

API ready sur `http://localhost:5000`
