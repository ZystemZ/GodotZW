# Godot Rev Zystem v0.13.6 — Windows x64

**Pre-release.** Cross-build Windows x64 concluído; os pacotes e checksums foram verificados. Esta versão ainda precisa de validação runtime em uma máquina Windows com LM Studio.

## Novidades e correções

- No modo **Somente leitura**, o schema disponibilizado ao provider inclui somente `list_project_files` e `read_file`; o painel também rejeita localmente chamadas `write_file`/`edit_file`.
- `list_project_files` usa `res://` automaticamente quando a chamada chega sem path, com string vazia ou placeholder `...`/`…`.
- `read_file` pode recuperar caminhos `res://...` citados explicitamente pelo usuário no pedido atual, em vez de tentar executar o placeholder do modelo. Se o modelo enviar uma chamada placeholder única para leitura, o painel pode expandi-la para os demais arquivos explicitamente pedidos, até oito leituras.
- Para um endpoint cujo host seja exatamente loopback (`localhost`, `127.0.0.1` ou `::1`), o agente recebe a raiz física atual do projeto conhecida pelo Godot.
- Nenhum destino ou conteúdo é adivinhado para escrita/edição. As ferramentas continuam sujeitas à resolução central de paths e às verificações de segurança do Workspace.

## Teste no LM Studio

Abra um projeto descartável, configure o endpoint local do LM Studio, por exemplo `http://127.0.0.1:1234/v1`, escolha **Somente leitura** e peça para listar a raiz e ler paths explícitos como `res://Main.gd` e `res://Player.gd`. O esperado é listar e ler esses arquivos mesmo que o modelo retorne placeholders; nenhum arquivo deve ser alterado. Se o servidor local bloquear a requisição, confira CORS no LM Studio e a autorização do endpoint no firewall do Windows.

## Build e validação

Build cruzado MinGW-w64/SCons: exit code 0. O executável GUI é PE32+ x86-64. Checks estáticos direcionados passaram. CRC dos ZIPs, hashes e igualdade byte a byte dos fontes C++ incluídos no pacote de fontes foram verificados. A resposta real do usuário em v0.13.4 já havia demonstrado listagem da raiz Windows `W:/bfep/futebol-3d-godot-4`, mas isso não constitui validação runtime da v0.13.6.

**Runtime v0.13.6 no Windows/LM Studio: pendente.** Use um projeto descartável e revise qualquer prévia antes de autorizar alterações.

## Arquivos

- `Godot-Rev-Zystem-v0.13.6-Windows-x64.zip`
- `Godot-Rev-Zystem-v0.13.6-Windows-x64.exe`
- `Godot-Rev-Zystem-v0.13.6-Windows-x64.console.exe`
- `Godot-Rev-Zystem-v0.13.6-Fontes.zip`
- `SHA256SUMS-v0.13.6.txt`
