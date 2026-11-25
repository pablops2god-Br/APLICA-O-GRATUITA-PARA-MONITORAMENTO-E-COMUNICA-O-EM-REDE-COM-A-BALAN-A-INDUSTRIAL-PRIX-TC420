# PRIX TC420

Aplicação desktop em Python para monitorar o terminal de pesagem PRIX TC420.
Desenvolvida por **Pablops2god**. Versão atual: **0.0.1**.

## Funcionamento

- HTTPS: aquisição autenticada na TC420; o computador PRINCIPAL distribui
  configuração e leituras aos CLIENTES da rede local.
- TCP e UDP entre computadores: distribuição TCP na porta 42100 e descoberta
  UDP na porta 42101, com sucessão condicionada às provas de encerramento.
- TCP direto: monitoramento local do peso, com porta inicial 9800, sem criar
  servidor ou participar da sucessão. Esse parser não fornece tara ou limites.
- Interface Tkinter, controle administrativo, exportação manual do histórico
  retido e acompanhamento do encerramento de recursos.

## Executar no Windows

O ambiente de build documentado usa Python 3.13. Outros ambientes precisam
de validação própria. Tkinter deve estar disponível na instalação do Python.

```powershell
py -3.13 -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe main.py
```

Cadastre a senha administrativa e configure o endereço real do seu equipamento
pela interface. A cópia preparada para publicação usa endereços demonstrativos
da faixa 192.0.2.0/24 no lugar dos endereços operacionais identificados.
Credenciais e configurações locais não acompanham essa cópia.

## Testes e laboratório visual

```powershell
.\.venv\Scripts\python.exe -m pip install -r requirements-dev.txt
.\.venv\Scripts\python.exe -m unittest discover -s tests -p "test_*.py"
.\.venv\Scripts\python.exe tests/ensaio_visual_tk.py
```

A suíte usa cenários controlados e inclui ensaios com sockets em localhost.
O laboratório é uma demonstração offline. `tc420.py` e `teste_approval.py`
são scripts manuais legados que podem acessar um equipamento real; não são
o ponto de entrada gráfico nem o comando de regressão acima.

## Organização

| Pasta | Responsabilidade |
|---|---|
| `config/` | Configuração, caminhos e administração |
| `tc420/` | Acesso ao equipamento e interpretação |
| `rede/` | Servidor, cliente, descoberta, supervisão e TCP local |
| `interface/` | Janelas, notificações, histórico e encerramento |
| `assets/` | Imagens utilizadas pela interface |
| `tests/` | Regressões, laboratório e ferramentas de medição |
| `prototipos/` | Experimentos e componentes referenciados pelo código e testes |
| `empacotamento/` | Fontes de build e configuração manual de firewall |
| `documentação/` | Contratos, operação, resultados e limitações |
| `ferramentas/` | Preparação reproduzível da cópia de publicação |

Alguns componentes de `prototipos/` são importados pelo aplicativo ou pela
regressão; a pasta deve acompanhar o código. Sua presença não significa que
todas as propostas experimentais foram integradas ao produto.

## Distribuição e limitações

Consulte [executável Windows](documentação/EXECUTAVEL_WINDOWS.md) e
[firewall](documentação/FIREWALL_WINDOWS.md). O repositório contém fontes
de empacotamento; executáveis e ambientes de build ficam fora do código.
Scripts de firewall exigem elevação somente quando executados explicitamente.
Instalador, desinstalador, assinatura e log automático permanecem pendentes
no corte documentado. O build anterior não substitui teste em Windows limpo.

O HTTPS atual desativa a validação do certificado; o canal entre computadores
não possui autenticação ou criptografia de aplicação. A descoberta não garante
um único PRINCIPAL sob partição de rede. O programa não calibra nem homologa
o equipamento e deve ser validado no ambiente de uso.

## Publicação e direitos

Veja [seleção para GitHub](documentação/PUBLICACAO_GITHUB.md). A cópia de
publicação é separada do histórico Git local e não contém dados de conexão,
cadastro administrativo, conversas, coletas brutas, backups ou builds.

Uma licença de distribuição do código ainda não foi definida pelo autor.
A disponibilização do repositório não deve ser descrita como concessão de
licença MIT, GPL ou equivalente sem decisão explícita. Imagens e identificação
do equipamento Toledo/PRIX pertencem aos respectivos titulares; sua inclusão
não transfere direitos sobre marcas ou conteúdo do fabricante.

Manual do equipamento: [TC420 — Toledo do Brasil](https://www.toledobrasil.com/blob/manuals/156_pt_manual_1723821221.pdf).
