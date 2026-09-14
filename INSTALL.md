# 🏛️ Guia de Instalação e Contribuição: Repositório Público .github (IFB)
### Instituto Professor Doutor Fernando Afonso Bonillo Fernandes (IFB)
**Governança Técnica:** CTO Itaymberê Guimarães (ISNI-26080506082) (@suporte / @itaymbere)  
**Gestão Executiva:** Diretor-Presidente Diego Toledo Fernandes (@presidencia / @diego)  
**Repositório Oficial:** [`Instituto-Fernando-Bonillo/.github`](https://github.com/Instituto-Fernando-Bonillo/.github)  

---

## 🎯 1. Visão Geral do Repositório

O repositório público **`.github`** centraliza a identidade visual pública da organização no GitHub, os modelos padronizados de abertura de chamados (Issue Templates), o código de conduta comunitário e os fluxos de trabalho de integração contínua (GitHub Actions) públicos do **Instituto Fernando Bonillo**.

### Conteúdo Estrutural:
* `profile/README.md` — Página de apresentação oficial da organização no GitHub.
* `.github/ISSUE_TEMPLATE/` — Modelos para abertura de tarefas, bugs, ideias e parcerias.
* `.github/workflows/` — Automações de validação de Markdown e verificação de links.
* `CONTRIBUTING.md` — Diretrizes para desenvolvedores voluntários e colaboradores.
* `CODE_OF_CONDUCT.md` — Código de conduta pautado nos princípios *Ubuntu* e *Ikigai*.

---

## 📋 2. Requisitos de Ambiente

* **Git:** 2.30 ou superior.
* **GitHub CLI (`gh`):** Para testes de workflows e gerenciamento de issues.
* **Node.js (Opcional):** Para formatação com `prettier` ou lint com `markdownlint`.
* **Act (Opcional):** Para executar localmente os fluxos do GitHub Actions via Docker/Podman.

---

## 🐧 3. Instalação e Execução no Linux Debian 13 (Trixie)

### 3.1. Instalar Ferramentas Básicas
```bash
sudo apt update && sudo apt install -y git curl wget
```

### 3.2. Instalar o GitHub CLI (`gh`)
```bash
(type -p wget >/dev/null || (sudo apt update && sudo apt install wget -y)) \
  && sudo mkdir -p -m 755 /etc/apt/keyrings \
  && out=$(mktemp) && wget -nv -O$out https://cli.github.com/packages/githubcli-archive-keyring.gpg \
  && cat $out | sudo tee /etc/apt/keyrings/githubcli-archive-keyring.gpg > /dev/null \
  && sudo chmod go+r /etc/apt/keyrings/githubcli-archive-keyring.gpg \
  && echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null \
  && sudo apt update \
  && sudo apt install gh -y
```

### 3.3. Autenticar no GitHub
```bash
gh auth login
```

### 3.4. Clonar o Repositório
```bash
git clone https://github.com/Instituto-Fernando-Bonillo/.github.git ifb-public-github
cd ifb-public-github
```

### 3.5. Validar os Arquivos Markdown Localmente
Caso deseje validar links e sintaxe:
```bash
# Instalação rápida de linter Markdown
sudo apt install -y npm && sudo npm install -g markdownlint-cli
markdownlint **/*.md
```

---

## 🍏 4. Instalação e Execução no macOS v27 (ou Superior / Homebrew)

### 4.1. Instalar Ferramentas via Homebrew
```bash
brew install git gh markdownlint-cli
```

### 4.2. Autenticar e Clonar
```bash
gh auth login
git clone https://github.com/Instituto-Fernando-Bonillo/.github.git ifb-public-github
cd ifb-public-github
```

### 4.3. Testar Workflows Localmente com `act` (Opcional)
Se o Docker Desktop ou OrbStack estiver instalado no macOS:
```bash
brew install act
act -l
```

---

## 🪟 5. Instalação e Execução no Windows 10 (com WampServer Instalado)

No ambiente Windows 10, mesmo que o WampServer esteja primariamente dedicado a serviços Apache/PHP/MySQL, o desenvolvedor pode utilizar o Git Bash ou PowerShell para manter e validar os arquivos deste repositório.

### 5.1. Instalar Utilitários no Windows 10
Abra o **PowerShell como Administrador**:
```powershell
# Instalar Git e GitHub CLI
winget install --id Git.Git -e
winget install --id GitHub.cli -e

# (Opcional) Instalar Node.js para validação de Markdown
winget install --id OpenJS.NodeJS.LTS -e
```
*Reinicie o PowerShell após a conclusão das instalações.*

### 5.2. Autenticar no GitHub
No PowerShell ou Git Bash:
```powershell
gh auth login
```

### 5.3. Clonar o Repositório
Recomenda-se clonar dentro de sua pasta de trabalho (ex: `C:\Projetos` ou `C:\wamp64\www`):
```powershell
cd C:\wamp64\www
git clone https://github.com/Instituto-Fernando-Bonillo/.github.git ifb-public-github
cd ifb-public-github
```

### 5.4. Validar Markdown e Visualizar Localmente
Se possuir o Node.js instalado:
```powershell
npm install -g markdownlint-cli
markdownlint profile\README.md README.md
```

Para visualizar a renderização do perfil antes de enviar o commit, você pode usar extensões do Visual Studio Code (como *Markdown Preview Enhanced*) ou testar diretamente através de um branch pessoal com `gh pr create`.

---

## 🚀 6. Fluxo de Envio de Contribuições (Git Workflow)

1. Crie uma branch temática:
   ```bash
   git checkout -b feature/melhoria-perfil-institucional
   ```
2. Realize as modificações necessárias respeitando as diretrizes institucionais do IFB.
3. Crie o commit seguindo o padrão semântico:
   ```bash
   git commit -m "docs: atualiza dados do conselho supremo no perfil institucional"
   ```
4. Envie a branch e abra o Pull Request:
   ```bash
   git push origin feature/melhoria-perfil-institucional
   gh pr create --title "Atualização do Perfil Público" --body "Adequação dos dados institucionais."
   ```
