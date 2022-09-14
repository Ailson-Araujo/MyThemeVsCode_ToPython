# Ambiente Python no VSCode

## Instalação de Tema pessoal baseado no Drácula e Community Material Theme.

1. Instale o tema Drácula no VSCode.

2. Execute um dos comandos abaixo e localize a pasta do tema drácula.
    - **Linux** `~/.vscode/extensions`
    - **macOs** `~/.vscode/extensions`
    - **Windows** `%USERPROFILE%\.vscode\extensions`
  
3. Substitua os dados do arquivo *"dracula.json"* pelos dados do [Settings_Dracula](https://github.com/Ailson-Araujo/MyThemeVsCode_ToPython/blob/main/Settings_Dracula.json)

4. Substitua os dados de Configuração do VSCode: *"settings.json"* pelos dados do [Setting_VSCode](https://github.com/Ailson-Araujo/MyThemeVsCode_ToPython/blob/main/Setting_VSCode.json). Os dados de configurações podem ser verificados precionando a tecla **F1**, em seguida digitar setting e selecionar a primeira opção exibida.

<details>
<summary><h2>Instalação do ZSH</summary>

1. Instale o WSL2 conforme [página oficial](https://docs.microsoft.com/pt-br/windows/wsl/install)
2. Após instalado e atualizado a distro do WSL com os camandos `sudo apt updade -y` e `sudo apt upgrade -y` seguimos com a instalação do ZSH executando os seguintes comandos:
   - `sudo apt install zsh -y`
   - `sudo apt-get install powerline fonts-powerline -y`
   - `chsh -s /bin/zsh`
   
   Feche o terminal e abra-o novamente. Após aparecer uma tela com opções digite a letra: **q**
   
   ```
   sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
   ```
   
3. Instalação de Tema.
   
   - Tema [Spaceship ZSH](https://github.com/spaceship-prompt/spaceship-prompt)
   ```
   git clone https://github.com/spaceship-prompt/spaceship-prompt.git "$ZSH_CUSTOM/themes/spaceship-prompt" --depth=1
   ```
   
   - Criação de link simbólico para o tema
   ```
   ln -s "$ZSH_CUSTOM/themes/spaceship-prompt/spaceship.zsh-theme" "$ZSH_CUSTOM/themes/spaceship.zsh-theme"
   ```
4. Instalação de Plugins.
   
   - Plugin de auto complete [autosuggestions](https://github.com/zsh-users/zsh-autosuggestions/blob/master/INSTALL.md)
   ```
   git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
   ```
   
   - Plugin de destaque [highlighting](https://github.com/zsh-users/zsh-syntax-highlighting/blob/master/INSTALL.md)
   ```
   git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
   ```
   
5. Ativando tema e plugins.
   - Execute o comando `nano ~/.zshrc` para editar o arquivo de configuração.
   - Localize a variável `ZSH_THEME` e atribua o valor *"spaceship"* ficando dessa forma `ZSH_THEME="spaceship"`
   - Localize a variável `plugins=(git)` e acrescente os novos plugins *zsh-autosuggestions* e *zsh-syntax-highlighting* ficando desta forama: `plugins=(git zsh-autosuggestions zsh-syntax-highlighting)` feito as alterações precione `Ctrl` + `O` para salvar e `Ctrl` + `X` para sair.

## Integrando ZSH como shell no VSCode Windows

```

"terminal.integrated.profiles.windows": {
    "ZSH":{
        "path": "C:\\Windows\\System32\\bash.exe",
        "args": ["-c", "zsh"],
        "icon": "terminal"
    },
},
    
"terminal.integrated.defaultProfile.windows": "ZSH",
```
</details>


<details>
<summary><h2>Instalação do FISH</summary>

1. Instale o WSL2 conforme [página oficial](https://docs.microsoft.com/pt-br/windows/wsl/install)
2. Após instalado e atualizado a distro do WSL com os camandos `sudo apt updade` e `sudo apt upgrade` seguimos com a instalação do **Fish** executando os seguintes comandos:

   - `sudo apt install fish`
   - `sudo apt-get install powerline fonts-powerline`
   - `chsh -s /usr/bin/fish`
   
3. Instalação de Tema.

   - Gerenciador de Temas [Oh My Fish](https://github.com/oh-my-fish/oh-my-fish)
   
   - `curl -L http://get.oh-my.fish | fish`
   
   ### Tema Defaut
   
   - `omf install eclm`
   
   - Alguns comandos do Gerenciador:
   
       ```
       > omf install [<name>|<url>] // Instalando um plugin  
       > omf list // Lista os pacotes instalados   
       > omf theme // Lista os temas intalados   
       > omf theme [<name>] // Muda para o tema informado   
       > omf remove [<name>] // Remove um pacote
       ```
   
   ### Tema [Starship](https://starship.rs/)
   
   - Baixe a [fonte Nerd Fira Code](https://www.nerdfonts.com/) e instale no seu terminal:
   
        VSCode:
        ```
        "terminal.integrated.fontFamily": "FiraCode NF",
        "terminal.integrated.fontSize": 14
        ```
    
        Windows Terminal:
        ```
        "defaults": {
            "fontFace": "FiraCode NF",
            "fontSize": 11
        },
        ```
   - Instale o tema **Starship**
   
       `curl -sS https://starship.rs/install.sh | sh`
       
   - Defina o tema para iniciar junto com o terminal
   
       `code ~/.config/fish/config.fish`
       
       No arquivo aberto adicione: `starship init fish | source` e salve o arquivo.
       

4. Configuração
   
   Crie o arquivo: `code ~/.config/starship.toml`
       
   Adicione o seguinte codigo:
       
       ```
       # Get editor completions based on the config schema
       "$schema" = 'https://starship.rs/config-schema.json'

       # Inserts a blank line between shell prompts
       add_newline = true

       # Replace the "❯" symbol in the prompt with "➜"
       [character] # The name of the module we are configuring is "character"
       success_symbol = "[➜](bold green)" # The "success_symbol" segment is being set to "➜" with the color "bold green"

       # Disable the package module, hiding it from the prompt completely
       [package]
       disabled = true

       ```
       
   - Personalização de Simbolos
   
       No mesmo arquivo acima podem ser adicionado o codigo abaixo:
       
       ```
       [aws]
       symbol = "  "

       [buf]
       symbol = " "
       
       [c]
       symbol = " "
       
       [conda]
       symbol = " "
       
       [dart]
       symbol = " "
       
       [directory]
       read_only = " "
       
       [docker_context]
       symbol = " "
       
       [elixir]
       symbol = " "
       
       [elm]
       symbol = " "
       
       [git_branch]
       symbol = " "
       
       [golang]
       symbol = " "
       
       [haskell]
       symbol = " "
       
       [hg_branch]
       symbol = " "
       
       [java]
       symbol = " "
       
       [julia]
       symbol = " "
       
       [memory_usage]
       symbol = " "
       
       [nim]
       symbol = " "
       
       [nix_shell]
       symbol = " "
       
       [nodejs]
       symbol = " "
       
       [package]
       symbol = " "
       
       [python]
       symbol = " "
       
       [spack]
       symbol = "🅢 "
       
       [rust]
       symbol = " "

       ```
</details>
   
