# Guia Leonilson

Se precisar consultar [Markdown](https://www.markdownguide.org/cheat-sheet/)

[Acessar Linux](#Linux)

[Acessar Windows](#Windows)

[Acessar Informações complementares](#complementares)

### Configuração de Software

&nbsp; Teste de paragrafo

## Linux
* sudo apt uptade (busca atualizações)
* sudo apt upgrade (instala atualizações)
* sudo apt install (instala aplicativos baixados no sistema ou em repositorios previamente instalados)
## Windows

## Informações complementares


markdown_content = """# Guia Técnico: Manutenção, Diagnóstico de Software e Administração de Sistemas

Este repositório contém o resumo consolidado das competências abordadas na disciplina de **Manutenção e Configuração de Software** do curso de *Técnico em Manutenção e Suporte em Informática* (IFB Campus Taguatinga). O conteúdo abrange administração de sistemas Linux, diagnóstico de falhas em ambiente Windows, identificação de malwares e estratégias de manutenção preventiva, corretiva e preditiva.

---

## 1. Comandos e Administração de Sistemas Linux

A administração eficiente do Linux via CLI (Linha de Comando) envolve comandos fundamentais para manipulação de arquivos e diretórios, além de ferramentas robustas para análise de disco e políticas de backup.

### 1.1 Manipulação de Arquivos e Pastas
* `mkdir <nome>`: Cria uma nova pasta vazia no diretório atual ou no caminho especificado.
* `rmdir <nome>`: Remove uma pasta, desde que esta esteja completamente vazia.
* `rm <arquivo>`: Exclui arquivos individuais do sistema.
* `rm -r <pasta>`: Remove de forma recursiva uma pasta e todo o seu conteúdo interno (subpastas e arquivos).
* `cp <origem> <destino>`: Copia arquivos ou pastas de uma origem para um diretório de destino.
* `mv <origem> <destino>`: Move arquivos ou pastas entre diretórios. Também é utilizado para renomear itens caso permaneçam no mesmo local.
* `nano <arquivo>`: Editor de texto simples baseado em terminal, ideal para edições rápidas de arquivos de configuração.
* `cat <caminho>`: Exibe o conteúdo completo de um arquivo de texto simples diretamente no terminal.

### 1.2 Análise de Armazenamento e Limpeza de Disco
* **Interface Gráfica (Baobab):** O *Disk Usage Analyzer* fornece um mapa visual radial e estruturado para identificar rapidamente quais diretórios ou arquivos estão consumindo a maior parte do armazenamento. Instalação via terminal: `sudo apt install baobab`.
* `df -h`: Exibe o uso geral do espaço em disco de todos os sistemas de arquivos montados, utilizando um formato de leitura humana (human-readable, ex: GB, MB).
* `du -h --max-depth=1 ~` ou `/`: Analisa o uso detalhado do espaço em disco por pastas, limitando a exibição ao primeiro nível de profundidade a partir do diretório escolhido (Home ou Raiz).
* **Busca Avançada de Arquivos Pesados:** O comando `sudo du -ah / | sort -rh | head -n 10` lista de forma ordenada os 10 maiores arquivos ou diretórios do sistema, permitindo localizar rapidamente os vilões do armazenamento.
* **Limpeza Rápida de Pacotes:**
  * `sudo apt autoremove`: Remove automaticamente pacotes e dependências órfãs que foram instalados com outros programas e não são mais necessários no sistema.
  * `sudo apt clean`: Limpa o cache local de arquivos de pacotes baixados (.deb), liberando espaço na partição do sistema.

### 1.3 Estratégia de Backup Automatizado com Déjà Dup
O Déjà Dup é uma ferramenta utilitária integrada e simplificada para a realização de backups automáticos e agendados no ecossistema Linux (frequentemente listada no menu como "Backups").
* **Instalação:** `sudo apt update && sudo apt install deja-dup`
* **Configuração de Escopo:** Permite especificar detalhadamente quais pastas devem ser protegidas (ex: `/home`) e quais devem ser ignoradas pelo processo de salvamento (ex: `/Downloads` e diretórios de lixeira).
* **Destinos de Armazenamento:** Suporta o salvamento em mídias físicas locais (HDs externos, pendrives) ou diretamente em servidores de nuvem compatíveis (como o Google Drive).
* **Segurança Crítica via Criptografia:** É fundamental ativar a criptografia e definir uma senha robusta durante a configuração inicial. Sem essa senha configurada pelo técnico, o acesso posterior e a restauração dos dados tornam-se completamente impossíveis em caso de desastre.
* **Comportamento Incremental:** Após a realização do primeiro backup completo (que costuma demandar mais tempo), as execuções subsequentes operam de forma incremental, salvando apenas as modificações recentes e otimizando o uso do armazenamento.

---

## 2. Diagnóstico de Problemas de Software (Ambiente Livre de Malware)

Nem toda instabilidade ou travamento em um sistema operacional decorre de uma infecção por vírus. O trabalho do suporte técnico exige classificar corretamente os sintomas e empregar utilitários nativos para identificar a causa raiz.

### 2.1 Classificação e Tipos de Falhas
1. **Bug:** Ocorre quando um programa trava, apresenta comportamento anômalo contínuo ou fecha sozinho inesperadamente (crash) durante a utilização rotineira.
2. **Configuração:** O aplicativo falha em inicializar ou apresenta erros devido a parâmetros de sistema incorretos armazenados em seus registros ou arquivos de inicialização.
3. **Dependência:** A ausência ou corrupção de uma biblioteca dinâmica essencial (como arquivos .dll no ecossistema Windows), framework ou componente compartilhado impede a execução do software.
4. **Desempenho:** Sobrecarga severa de recursos físicos do hardware (como uso de CPU ou memória RAM fixados em 100%), gerando extrema lentidão ou congelamento temporário do sistema operacional.
5. **Serviço:** Um serviço vital executado em segundo plano (background) pelo sistema operacional parou de funcionar ou falhou em iniciar corretamente, desativando funções dependentes.

### 2.2 Utilitários Nativos do Windows para Investigação Crítica
* **Gerenciador de Tarefas (`Ctrl + Shift + Esc`):** Fornece monitoramento em tempo real do consumo de processamento, memória, disco e rede. É a ferramenta primária para identificar quais processos estão consumindo recursos de forma anormal.
* **Visualizador de Eventos (`eventvwr`):** Consiste no registro histórico centralizado de todas as ocorrências do sistema operacional. Ele armazena logs detalhados de aplicativos, segurança e eventos críticos do sistema. É indispensável para rastrear a causa raiz de erros que fecham programas "silenciosamente" sem exibir mensagens na tela.
* **Gerenciador de Serviços (`services.msc`):** Interface para controle de processos em segundo plano. Permite iniciar, parar, reiniciar e configurar o comportamento de inicialização de serviços do Windows (Automático, Manual ou Desativado), além de parametrizar ações automáticas de recuperação em caso de falha do serviço.
* **Prompt de Comando (CMD) - Comandos Avançados de Rede e Processos:**
  * `ipconfig /all`: Exibe a configuração detalhada de todas as interfaces de rede ativas na máquina.
  * `ipconfig /release` e `ipconfig /renew`: Executam, respectivamente, a liberação e a renovação do endereço de IP obtido via servidor DHCP.
  * `tasklist`: Lista todos os processos em execução no sistema operacional em formato de tabela, revelando seus nomes exatos e seus respectivos PIDs (*Process IDs*).
  * `taskkill /IM nome_do_programa.exe /F` ou `taskkill /PID <número> /F`: Força o encerramento imediato e definitivo de um processo travado na memória que recusa o fechamento padrão.

---

## 3. Identificação, Diagnóstico e Solução de Malwares

Malwares (*Malicious Software*) são códigos ou programas desenvolvidos de forma intencional com o propósito de causar danos ao sistema, roubar informações credenciais, espionar a atividade do usuário ou garantir acessos não autorizados.

### 3.1 Os 5 Tipos Principais de Ameaças em Foco
1. **Ransomware (O Sequestrador):** Criptografa os arquivos do usuário, tornando-os completamente ilegíveis, e altera suas extensões originais (ex: `documento.docx` passa a ser `documento.docx.locked`). Simultaneamente, gera um arquivo de texto com instruções de resgate financeira (`LEIA-ME.txt`), geralmente exigindo pagamentos em criptomoedas.
2. **Keylogger (O Espião):** Monitora e registra de forma silenciosa cada tecla pressionada no teclado físico do computador. O seu principal impacto é o roubo invisível de credenciais de acesso, dados bancários e senhas, muitas vezes salvando as informações capturadas em arquivos ocultos que crescem continuamente (ex: `C:\Users\Public\log.txt`).
3. **Cryptojacker / Minerador (O Parasita):** Utiliza de forma oculta a capacidade de processamento do hardware (CPU e GPU) da vítima para realizar a mineração de criptomoedas em benefício do atacante. O sintoma mais visível é a máquina extremamente lenta, coolers barulhentos em velocidade máxima e uso de CPU travado em 100%, mesmo sem nenhum programa aberto na tela.
4. **Backdoor (A Porta dos Fundos):** Cria ou mantém uma abertura oculta no sistema operacional para que o invasor consiga retornar e controlar a máquina remotamente a qualquer momento, contornando completamente os mecanismos tradicionais de autenticação e firewalls.
5. **Trojan (O Cavalo de Troia / O Disfarçado):** Disfarça-se como um arquivo ou programa legítimo, útil ou inofensivo (como jogos gratuitos, utilitários, ativadores ou *cracks*) para induzir o usuário a realizar o download e a execução manual do código malicioso.

### 3.2 Metodologia de Investigação e Ferramentas de Análise
Para realizar o diagnóstico correto de uma infecção, o técnico deve analisar o comportamento do sistema através de ferramentas nativas:
* **Em Ambiente Windows:**
  * **Gerenciador de Tarefas (Aba Detalhes):** Permite inspecionar os processos ativos em segundo plano. É crucial para identificar executáveis com nomes genéricos, sem descrição de fabricante ou que mimetizam processos legítimos com pequenos erros ortográficos (ex: `svchost.exe` rodando sob permissões de usuário comum em pastas temporárias como `AppData` ou `Temp`).
  * **Monitor de Recursos (`resmon`):** Utilizado para mapear detalhadamente o tráfego de rede gerado por processos específicos e verificar a atividade oculta de escrita em disco.
  * **Prompt de Comando (`netstat -ano`):** Exibe todas as conexões de rede ativas e portas em estado de escuta (`LISTENING`), vinculando cada porta ao PID do processo responsável. Portas incomuns ativas (ex: porta 4444) funcionam como fortes evidências de *backdoors*.
* **Em Ambiente Linux:**
  * `top` ou `htop`: Exibe o uso de processamento e memória RAM por processo em tempo real.
  * `netstat -an`: Lista as portas de rede abertas e conexões estabelecidas.
  * `ps aux`: Fornece uma listagem detalhada e estática de todos os processos em execução no sistema.
  * `lsof -i`: Mapeia quais arquivos e processos estão associados a conexões de rede específicas.

> **Técnica Avançada: Living off the Land (LotL)**
> Atacantes modernos frequentemente desenvolvem malwares baseados em scripts nativos (como PowerShell no Windows ou Python no Linux) que utilizam ferramentas legítimas do próprio sistema para executar ações danosas. Como essas ferramentas já são confiáveis, os antivírus tradicionais baseados em assinatura estática de arquivos podem não emitir alertas. Por isso, ferramentas de monitoramento comportamental (como soluções EDR) são indispensáveis no ambiente corporativo.

---

## 4. Metodologias e Práticas de Manutenção de Software

A realização de rotinas periódicas de manutenção de software previne o acúmulo de arquivos desnecessários, corrige vulnerabilidades operacionais e prolonga o ciclo de vida do hardware.

### 4.1 Os Três Tipos de Manutenção Técnica
* **Manutenção Preventiva (Agir Antes):** Consiste em ações planejadas e periódicas executadas antes do surgimento de qualquer erro, visando mitigar riscos e otimizar o desempenho. *Exemplos:* Limpeza programada de arquivos temporários, varreduras completas com antivírus e aplicação regular de patches do sistema.
  * *Nota de Impacto Histórico:* O ataque global do ransomware WannaCry em 2017 explorou a vulnerabilidade *EternalBlue*. A Microsoft havia disponibilizado o patch de segurança (MS17-010) 59 dias antes do surto. Organizações que aplicavam rotinas de manutenção preventiva ficaram completamente imunes ao ataque.
* **Manutenção Corretiva (Agir Depois):** Intervenção técnica realizada de modo reativo após a manifestação de uma falha ou parada no sistema, com o objetivo de restaurar a normalidade operacional o mais rápido possível. *Exemplos:* Reinstalação de um sistema de arquivos corrompido, aplicação de comandos de reparo ou remoção ativa de um malware detectado.
* **Manutenção Preditiva (Antecipar Falhas):** Baseia-se no monitoramento constante e sistemático de métricas comportamentais do computador para diagnosticar indícios de falhas estruturais futuras antes que elas ocorram. *Exemplos:* Acompanhamento de logs críticos recorrentes no Visualizador de Eventos, análise das temperaturas de operação do processador e verificação dos parâmetros de integridade física S.M.A.R.T. de discos rígidos e SSDs.

### 4.2 Ferramentas Nativas de Otimização no Windows
1. **Limpeza de Disco (`cleanmgr`):** Utilitário para exclusão de arquivos de log antigos, cache de miniaturas e arquivos temporários de instalação. Ao acionar a opção profissional "Limpar arquivos do sistema", o técnico consegue remover gigabytes de atualizações antigas acumuladas pelo Windows Update e a pasta `Windows.old`. *Recomendação Técnica:* Nunca exclua a pasta `Windows.old` imediatamente após um upgrade de sistema sem antes garantir que todos os softwares essenciais da máquina estão operando perfeitamente, pois ela é necessária para a realização de um *rollback* (retorno à versão anterior).
2. **Pasta Temporária de Usuário (`%temp%`):** Diretório acessado via comando Executar (`Win + R`), responsável por armazenar arquivos temporários gerados pelo perfil do usuário logado. Diferente do `cleanmgr`, essa pasta exige limpeza manual frequente. Arquivos que estiverem em uso ativo pelo sistema operacional no momento da exclusão serão ignorados automaticamente, o que configura um comportamento normal.
3. **Windows Update:** Ferramenta crítica de manutenção preventiva e segurança. Ela distribui correções de vulnerabilidades (*patches*), correções de estabilidade de código e atualizações de drivers de fabricantes para manter a compatibilidade do hardware. A melhor prática em ambientes corporativos dita que as atualizações automáticas devem ser gerenciadas e agendadas para horários fora do expediente comercial, e nunca desativadas por completo.
4. **Windows Defender (`windowsdefender`):** Antivírus integrado e nativo do Windows. Oferece três modalidades essenciais de varredura: **Verificação Rápida** (inspeciona processos ativos na memória e registros do sistema, levando de 2 a 5 minutos; indicada para rotinas diárias), **Verificação Completa** (examina minuciosamente todos os setores de armazenamento do disco) e **Verificação Personalizada** (direcionada a mídias removíveis ou pastas específicas indicadas pelo usuário). *Alerta Técnico:* Caso o Windows Defender se encontre desativado sem nenhuma justificativa ou intervenção deliberada do administrador, isto representa um forte indicador de que um malware desabilitou a proteção ativa para operar de forma oculta.
5. **Verificador de Arquivos do Sistema (`sfc /scannow`):** Comando avançado executado obrigatoriamente através do Prompt de Comando (CMD) aberto sob credenciais de Administrador. Ele varre a integridade de todos os arquivos de sistema protegidos e repara cópias corrompidas de forma autônoma. Caso a ferramenta relate que encontrou arquivos corrompidos mas não conseguiu reparar alguns deles, o técnico deve executar em seguida o comando complementar do DISM: `DISM /Online /Cleanup-Image /RestoreHealth` para reconstruir a imagem base de arquivos do Windows a partir dos servidores oficiais da Microsoft.
6. **Aba Inicialização do Gerenciador de Tarefas:** Permite inspecionar e desabilitar programas que carregam automaticamente ao ligar o computador, reduzindo significativamente o tempo de boot e liberando memória RAM. Deve-se manter habilitados apenas softwares antivírus, drivers de hardware e ferramentas corporativas essenciais.

---

## 5. Tomada de Decisão e Gestão do Ciclo de Vida de Softwares

O papel de um técnico profissional em suporte de TI expande-se além do reparo prático, englobando a consultoria e a tomada de decisões técnicas fundamentadas sobre o ciclo de vida dos aplicativos da organização.

### 5.1 Critérios Técnicos para Decisão: Atualizar vs. Substituir
* **Deve-se Atualizar o Software quando:**
  * Há uma versão mais recente e estável distribuída oficialmente pelo mesmo desenvolvedor.
  * O pacote de atualização mitiga vulnerabilidades de segurança documentadas ou soluciona bugs operacionais conhecidos.
  * O investimento financeiro na atualização é substancialmente inferior aos riscos operacionais e custos de segurança de manter a versão antiga e defasada ativa.
  * O parque de hardware instalado na organização atende aos novos requisitos mínimos exigidos pela nova versão do software.
* **Deve-se Substituir o Software quando:**
  * O desenvolvedor oficial declarou o encerramento do ciclo de vida do produto (EOL - *End of Life*).
  * O aplicativo deixou de receber quaisquer atualizações de segurança ou patches corretivos por um período superior a 12 meses.
  * Há uma incompatibilidade técnica crônica com os sistemas operacionais atuais ou futuros planejados pela empresa (ex: softwares legados que exigem exclusivamente o Windows 7 para operar).
  * Existem alternativas contemporâneas de código aberto (*open-source*) ou soluções modernas no mercado que ofereçam maior segurança, conformidade e um custo-benefício superior para o cenário específico da organização (ex: recomendar a migração do Microsoft Office comercial licenciado por máquina para o LibreOffice de código aberto em um contexto educacional ou de laboratório público, mantendo a compatibilidade funcional com formatos `.docx` sem custos de licenciamento recorrentes).
"""

file_path = "Guia_Tecnico_Manutencao_e_Diagnostico.md"
with open(file_path, "w", encoding="utf-8") as f:
    f.write(markdown_content)

print(f"File saved successfully to {file_path}")
