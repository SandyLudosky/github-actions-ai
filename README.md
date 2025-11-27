# AI-assisted CI/CD : Exécutez les Models IA dans les Github Actions

- Générer un résumé ou changelog intelligible du commit
```bash
Génère un résumé clair et concis des changements suivants :
${{ github.event.head_commit.message }}
```

- Analyser la qualité du code modifié
```bash
Analyse ce diff et signale les mauvaises pratiques potentielles,
les duplications et les risques de sécurité :
${{ steps.get-diff.outputs.diff }}
```

- Ajouter des tests unitaires
```bash
Analyse ce diff et signale les mauvaises pratiques potentielles,
les duplications et les risques de sécurité :
${{ steps.get-diff.outputs.diff }}
```
--

[1]- Python installation
[2]- Create and activate a virtual Environment
[3]- Install packages
[4]- Setting Up OpenAI Secret Key  
[5]- Intégrer les Github Models

### [1]-Python installation

#### macOS
1. **Check if Python is already installed**
   ```sh
   python3 --version
   ```
   If Python is not installed, proceed with the steps below.

2. **Install Homebrew (if not installed)**
   ```sh
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```

3. **Install Python**
   ```sh
   brew install python3
   ```

4. **Check Python Version**
   ```sh
   python3 --version
   ```

#### Windows
1. **Download Python** from the official website: [https://www.python.org/downloads/](https://www.python.org/downloads/)

2. **Run the installer** and check the box **"Add Python to PATH"** before proceeding with the installation.

3. **Check Python Version**
   ```sh
   python --version
   ```

---

### [2]-Create and activate a virtual environment - [venv](https://docs.python.org/3/library/venv.html)

#### macOS
1. **Navigate to your project directory**
   ```sh
   cd /path/to/your/project
   ```

2. **Create a virtual environment**
   ```sh
   python3 -m venv .venv
   ```

3. **Activate the virtual environment**
   ```sh
   source .venv/bin/activate
   ```

4. **Verify that the virtual environment is active** (you should see `(venv)` in the terminal prompt).

#### Windows
1. **Navigate to your project directory**
   ```sh
   cd C:\path\to\your\project
   ```

2. **Create a virtual environment**
   ```sh
   python -m venv .venv
   ```

3. **Activate the virtual environment**
   ```sh
   .venv\Scripts\activate
   ```

4. **Verify that the virtual environment is active** (Command Prompt should show `(venv)` before the directory path).

---

## Deactivating the Virtual Environment
For both macOS and Windows, deactivate the virtual environment by running:
```sh
 deactivate
```

---

### [3]-Install packages
(Mac)
```sh
pip3 install -r requirements.txt

export PYTHONPATH=$PYTHONPATH:/path/to/autogen_agentchat
```

(Windows)
```sh
pip install -r requirements.txt
```

---

## Exiting the Virtual Environment
Simply run:
```sh
deactivate
```

### [4]- Setting Up OpenAI Secret Key  
1. Create an OpenAI Account[OpenAI's API Keys page](https://platform.openai.com/signup/),
2. Go to [OpenAI's API Keys page](https://platform.openai.com/settings/organization/api-keys),
3. Click **Create new secret key** and copy it, 
4. You will need to add your billing information (MANAGE > Settings > Billing).  



#### Set environment variables 

##### macOS & Linux  
You can store the key in your shell configuration file:  

```sh
echo 'export OPENAI_API_KEY="your-secret-key"' >> ~/.bashrc
source ~/.bashrc
````

or add to `.env` file

```sh
OPENAI_API_KEY="YOUR_OPENAI_API_KEY"
GITHUB_TOKEN="YOUR_GITHUB_TOKEN"

```

### [5] - Intégrer les Github Models

#### *5.1 - Un compte personnel GitHub - [S'authentifier](https://github.com/login)
#### *5.2 - Créer un Personal Access Token (PAT) ou Fine-grained PAT - [Developer Settings](https://github.com/settings/personal-access-tokens)
#### *5.3 - Installer les modules et les SDK
#### *5.4 - Lancer un appel API - [**Guide de Démarrage**](https://docs.github.com/fr/github-models/quickstart)

```sh
echo 'export GITHUB_TOKEN="your-secret-key"' >> ~/.bashrc
source ~/.bashrc
````

```bash
curl -s \
  -X GET "https://models.github.ai/catalog/models" \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer $GITHUB_TOKEN" \
| jq
```

#### *5.5 - Models CLI

* [Github Models Extension](https://github.com/github/gh-models)
* Installer : `gh extension install https://github.com/github/gh-models`

(Mac)
```sh
brew install gh
```

(Windows)
```sh
winget install GitHub.cli
```

* Run Tests : 

`gh models run openai/gpt-4o-mini "what is 1 + 1"`


### -Start the app
(Mac)
```sh
python3 main.py
```

(Windows)
```sh
python main.py
```

