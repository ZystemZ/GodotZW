# GodotZW — Zystem integrado ao Godot

**GodotZW** é um fork experimental do Godot que integra o **ZystemWorkSpace**, um agente de programação em C++ nativo dentro do editor. Ele pode inspecionar o projeto e, conforme o modo de segurança, propor ou aplicar mudanças.

> **Versão atual: v0.13.6 (pre-release).** O editor Windows x64 foi compilado por cross-build e os pacotes foram verificados. A execução desta versão em Windows real com LM Studio ainda aguarda validação do usuário. Teste com um projeto descartável e faça backups.

## Downloads — v0.13.6

Os binários e o pacote completo de fontes são disponibilizados como assets da release, não como arquivos grandes no histórico Git:

- [Ver releases e downloads](https://github.com/ZystemZ/GodotZW/releases)
- [Release v0.13.6](https://github.com/ZystemZ/GodotZW/releases/tag/v0.13.6)

Assets publicados na release:

- `Godot-Rev-Zystem-v0.13.6-Windows-x64.zip` — pacote recomendado com os executáveis Windows x64 e documentação.
- `Godot-Rev-Zystem-v0.13.6-Windows-x64.exe` — editor GUI Windows x64.
- `Godot-Rev-Zystem-v0.13.6-Windows-x64.console.exe` — variante de console para diagnóstico.
- `Godot-Rev-Zystem-v0.13.6-Fontes.zip` — fontes completos e documentação/licenças.
- `SHA256SUMS-v0.13.6.txt` — hashes para conferir os executáveis e pacotes.

Consulte o manifesto `SHA256SUMS-v0.13.6.txt` anexado à release para os hashes SHA-256.

## Recursos atuais

- ZystemWorkSpace em C++ nativo e painel de IA que pode ficar no editor ou em uma janela flutuante.
- Providers compatíveis com OpenAI; consulta de modelos via `/v1/models` e seleção pelo ID publicado pelo provider.
- Tools de agente para listar e ler arquivos e, quando permitido, escrever e editar dentro do projeto. Paths relativos, paths Windows dentro da raiz e `res://` são aceitos.
- Modos Automático, Confirmar cada alteração e Somente leitura. No modo de confirmação, cada escrita/edição apresenta prévia e aguarda aprovação.
- Backups, journal transacional e controles de undo/redo, com bloqueio de divergências de conteúdo.
- Em Somente leitura, o provider recebe apenas ferramentas de listagem e leitura; paths res:// citados explicitamente podem ser recuperados quando o modelo retorna placeholder.
- A distribuição de fontes também contém o componente PHP complementar `ZystemWorkSpace`; requisitos em `README-REQUISITOS-PHP.md` dentro do pacote.

## Uso

1. Baixe o executável GUI na release e abra uma **cópia descartável** de um projeto Godot.
2. No painel **Zystem IA**, configure provider, endpoint, chave se necessária e modelo.
3. Use **Listar modelos** e selecione um ID retornado pelo provider.
4. Durante a validação, prefira **Confirmar cada alteração** ou **Somente leitura**. Revise cada prévia antes de aplicar.

Endpoints locais compatíveis podem incluir LM Studio (`http://127.0.0.1:1234/v1`) ou Ollama (`http://127.0.0.1:11434/v1`), conforme a configuração do provider instalado.
Dependendo da configuração do provider local, habilite CORS no LM Studio para permitir requisições do editor. Autorize o endpoint local no firewall do Windows se solicitado.

A configuração do Workspace pode conter uma API key em `res://.zystem/provider.cfg`. **Não publique essa pasta, chaves ou outros segredos.** O `.gitignore` exclui `.zystem/`, `ZystemWorkSpace/config/secrets.php`, `ZystemWorkSpace/config/admin.php`, `prompt_de_continuidade.txt` e `ROTEIRO-CONTINUIDADE-ORIGINAL.txt`. No pacote público, os arquivos locais `secrets.php` e `admin.php` são omitidos; seus exemplos ficam sem API key, usuário ou hash de senha. O prompt e o roteiro internos de continuidade também não são distribuídos.

## Código-fonte e build

O pacote de fontes da release contém a árvore Godot 4.8.0 beta usada no fork, as alterações do Zystem, o componente PHP e a documentação/licenças. O build Windows x64 foi compilado no Linux Sandbox com SCons e MinGW-w64 usando:

```sh
scons platform=windows target=editor arch=x86_64 use_mingw=yes d3d12=no accesskit=no angle=no -j2 progress=no
```

Consulte as notas da release v0.13.6 e `README-REQUISITOS-PHP.md` no pacote. As instruções oficiais e dependências de build do Godot estão na árvore de fontes incluída.

## Créditos e licenças

- **Projeto e integração Zystem:** ZystemZ.
- **Engine base:** Godot Engine, contribuidores do Godot Engine; autores originais Juan Linietsky e Ariel Manzur. O código upstream do Godot usa MIT/Expat, conforme `LICENSE.txt` e `COPYRIGHT.txt` incluídos no pacote.
- **Bibliotecas, fontes e demais componentes de terceiros:** cada componente conserva seus próprios avisos e licenças; consulte `COPYRIGHT.txt`, `thirdparty/README.md` e os arquivos de licença correspondentes na árvore de fontes.
- **Licença declarada deste repositório:** GNU GPL-3.0, conforme [`LICENSE`](LICENSE). Essa declaração não substitui nem remove os avisos/licenças de Godot ou de componentes de terceiros.

GodotZW é um fork independente e **não é um produto oficial nem é endossado pelo Godot Engine**. Consulte [CREDITS.md](CREDITS.md) para os créditos detalhados.
