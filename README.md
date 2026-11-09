# GodotZW — Zystem integrado ao Godot

**GodotZW** é um fork experimental do Godot que integra o **ZystemWorkSpace**, um painel nativo para conversar com um provider de IA compatível com a API OpenAI e pedir assistência diretamente dentro do editor.

> **Estado do projeto:** v0.13 foi cross-compilada para Windows x64 e verificada estaticamente. Ainda não foi validada em execução no Windows nem com providers reais. Use um projeto descartável e faça cópias de segurança.

## Downloads — v0.13

Os binários e o pacote completo de fontes são disponibilizados como assets da release, não como arquivos grandes no histórico Git:

- [Baixar a versão mais recente](https://github.com/ZystemZ/GodotZW/releases/latest)
- [Release v0.13](https://github.com/ZystemZ/GodotZW/releases/tag/v0.13)

Assets previstos na release:

- `Godot-Rev-Zystem-v0.13-Windows-x64.exe` — editor GUI Windows x64.
- `Godot-Rev-Zystem-v0.13-Windows-x64.console.exe` — variante de console para diagnóstico.
- `Godot-Rev-Zystem-v0.13-Fontes.zip` — código-fonte, componente PHP complementar, documentação, avisos/licenças e os binários.

SHA-256 do editor GUI: `1a02286907bd91289d0e51cbeab89a27fcca9595f6af3be95569a725b7d24995`.

## Recursos atuais

- ZystemWorkSpace em C++ nativo e painel de IA que pode ficar no editor ou em uma janela flutuante.
- Providers compatíveis com OpenAI; consulta de modelos via `/v1/models` e seleção pelo ID publicado pelo provider.
- Tools para listar e ler arquivos, além de criar/escrever e editar arquivos no projeto (`res://`).
- Modos Automático, Confirmar cada alteração e Somente leitura. No modo de confirmação, cada escrita/edição apresenta prévia e aguarda aprovação.
- Backups, journal transacional e controles de undo/redo, com bloqueio de divergências de conteúdo.
- O journal v0.13 associa à transação o prompt do turno atual, com até 1.200 caracteres e redação da API key configurada; snapshots anterior+posterior limitados a 262.144 caracteres combinados e retenção de até 100 transações concluídas.
- A distribuição de fontes também contém o componente PHP complementar `ZystemWorkSpace`; requisitos em `README-REQUISITOS-PHP.md` dentro do pacote.

## Uso

1. Baixe o executável GUI na release e abra uma **cópia descartável** de um projeto Godot.
2. No painel **Zystem IA**, configure provider, endpoint, chave se necessária e modelo.
3. Use **Listar modelos** e selecione um ID retornado pelo provider.
4. Prefira **Confirmar cada alteração** enquanto valida o comportamento. Revise cada prévia antes de aplicar.

Endpoints locais compatíveis podem incluir LM Studio (`http://127.0.0.1:1234/v1`) ou Ollama (`http://127.0.0.1:11434/v1`), conforme a configuração do provider instalado.

A configuração do Workspace pode conter uma API key em `res://.zystem/provider.cfg`. **Não publique essa pasta, chaves ou outros segredos.** O `.gitignore` exclui `.zystem/`, `ZystemWorkSpace/config/secrets.php`, `ZystemWorkSpace/config/admin.php`, `prompt_de_continuidade.txt` e `ROTEIRO-CONTINUIDADE-ORIGINAL.txt`. No pacote público, os arquivos locais `secrets.php` e `admin.php` são omitidos; seus exemplos ficam sem API key, usuário ou hash de senha. O prompt e o roteiro internos de continuidade também não são distribuídos.

## Código-fonte e build

O pacote de fontes da release contém a árvore Godot 4.8.0 beta usada na v0.13, as alterações do Zystem, o componente PHP e a documentação técnica/licenças. O build Windows x64 entregue foi compilado no Linux Sandbox com SCons e MinGW-w64 usando:

```sh
scons platform=windows target=editor arch=x86_64 use_mingw=yes d3d12=no accesskit=no angle=no -j2 progress=no
```

Consulte `BUILD-REPORT-WINDOWS-X64.txt` e `README-REQUISITOS-PHP.md` no pacote. As instruções oficiais e dependências de build do Godot estão na árvore de fontes incluída.

## Créditos e licenças

- **Projeto e integração Zystem:** ZystemZ.
- **Engine base:** Godot Engine, contribuidores do Godot Engine; autores originais Juan Linietsky e Ariel Manzur. O código upstream do Godot usa MIT/Expat, conforme `LICENSE.txt` e `COPYRIGHT.txt` incluídos no pacote.
- **Bibliotecas, fontes e demais componentes de terceiros:** cada componente conserva seus próprios avisos e licenças; consulte `COPYRIGHT.txt`, `thirdparty/README.md` e os arquivos de licença correspondentes na árvore de fontes.
- **Licença declarada deste repositório:** GNU GPL-3.0, conforme [`LICENSE`](LICENSE). Essa declaração não substitui nem remove os avisos/licenças de Godot ou de componentes de terceiros.

GodotZW é um fork independente e **não é um produto oficial nem é endossado pelo Godot Engine**. Consulte [CREDITS.md](CREDITS.md) para os créditos detalhados.
