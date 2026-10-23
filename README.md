# 🎮 GTA Cortes Automáticos — GitHub (grátis)

Monitoramento horário **somente de vídeos com GTA no título** publicados pelos canais oficiais do Flow Games, Cortes do Flow Games e GameplayRJ / Davy Jones. Para vídeos próprios ou autorizados, o projeto seleciona trechos por termos de GTA nas legendas/transcrição e cria até 2 MP4 verticais **1080 × 1920**, com áudio original, **sem legendas nem texto na tela**, sem banners, sem API paga e sem publicar automaticamente.

> **Status:** gerador e testes funcionam com arquivo local autorizado. O acesso automático a vídeos externos e à página do YouTube não é garantido. A execução de hora em hora é aproximada, pois o GitHub pode atrasá-la. Ainda não é uma instalação na sua conta: primeiro você precisa criar o repositório e adicionar estes arquivos.

## ⚠️ Direitos de uso

Flow Games, Cortes do Flow Games e GameplayRJ informam que **não autorizam a reutilização de seus vídeos, vozes e cortes sem permissão prévia**. Portanto:

- O **monitor** consulta somente metadados públicos e salva links das notícias de GTA; não baixa vídeo de terceiros.
- O **gerador MP4** só executa quando você fornece um URL que pode ser baixado/usar legitimamente **e confirma explicitamente os direitos**. Não marque a confirmação sem ter permissão ou direito de usar o material.
- A produção de cortes não é autorização para publicar. **Nada é postado** em Instagram, TikTok ou YouTube.
- Se o YouTube impedir o download, o passo falha e **nenhum MP4 será anunciado**.

## 📱 Instalar na sua conta GitHub pelo iPhone — jeito mais simples

1. Abra o repositório já criado pelo Safari no iPhone.
2. Use o repositório já criado em https://github.com/Alvar9/-gta-cortes-gratis (não é necessário criar outro).
3. A conexão GitHub atual pode permitir leitura sem permitir gravação. Use o navegador ou outra ferramenta Git autorizada para adicionar os arquivos do pacote ao repositório. Mantenha `.github/workflows/gta.yml`, `scripts/`, `data/` e os demais caminhos. Não envie só o ZIP: o GitHub precisa dos arquivos extraídos.
4. Depois que os arquivos forem enviados preservando a estrutura de pastas, abra seu repositório → **Actions** → **GTA — monitor e cortes gratuitos** → **Enable workflow**, se solicitado.
5. Para testar, toque em **Run workflow** com `video_url` vazio. Confira a etapa `Checar APENAS canais oficiais...` e o resumo da execução.
6. Para receber novidades, na página do repositório toque em **Watch** → notificações **Issues** (e habilite notificações do GitHub no seu e-mail/app). Se encontrar novidades de GTA ainda não vistas, o projeto cria uma *Issue*.

Não é preciso usar Codespaces, assinatura, API de IA paga, Runway ou vidIQ. GitHub pode ter restrições gerais de uso/armazenamento; o código não ativa serviços pagos.

## ✂️ Criar MP4 com vídeo autorizado

1. Abra **Actions** → **GTA — monitor e cortes gratuitos** → **Run workflow**.
2. Preencha `video_url` com o link do vídeo que você tem autorização para baixar e editar. Deve estar acessível para download pela ferramenta `yt-dlp`. É possível que URLs do YouTube falhem.
3. Marque `confirm_rights` **somente se possuir essa permissão**.
4. Abra a execução → **Artifacts** → **gta-cortes-mp4**. O download é um ZIP com arquivos MP4 e arquivos JSON com descrição e hashtags sugeridas. O ZIP expira após **7 dias**; salve os MP4 no aplicativo Arquivos/Fotos.

**Importante:** o download de artefatos fica dentro do **GitHub**, não diretamente no ChatGPT. Se quiser o MP4 neste chat, anexe o vídeo autorizado aqui para que o FFmpeg rode localmente; o projeto não promete anexá-lo automaticamente à conversa.

## 🛠️ Executar localmente em computador (opcional)

Requer Python 3.11+, FFmpeg, conexão para instalar dependências e, se usar `--url`, `yt-dlp`.

```bash
python -m pip install -r requirements.txt
python scripts/monitor.py
python scripts/clip.py --video "meu-video-autorizado.mp4" --confirm-rights --out output
```

Com arquivo de legenda para selecionar melhores trechos (a legenda **não aparece** no vídeo):

```bash
python scripts/clip.py --video "meu-video-autorizado.mp4" --subs "meu-video.srt" --confirm-rights --out output --count 2 --width 1080
```

Sem arquivo de legenda, o projeto transcreve o áudio localmente usando faster-whisper (download gratuito do modelo na primeira execução), apenas para selecionar os momentos. **Nunca insere texto no vídeo.**

## ⚙️ Como funciona

- `.github/workflows/gta.yml`: tentativa automática a cada hora, etapa manual de cortes.
- `channels.json`: IDs dos três canais oficiais.
- `scripts/monitor.py`: consulta feeds públicos RSS, aplica filtro GTA, registra IDs para não repetir notificações.
- `data/seen.json`: histórico deduplicado dos vídeos já identificados.
- `reports/novidades.md`: último relatório de **novas** publicações.
- `scripts/clip.py`: seleciona segmentos de fala com tema GTA (heurística por palavras), converte 9:16 com FFmpeg sem sobrepor legendas ou texto.
- `tests/test_pipeline.py`: testes de filtro, legendas e escolha de momentos.

A identificação de “melhor momento” é uma **heurística automatizada**, não uma avaliação editorial perfeita. Sempre confira o contexto e se é confirmação oficial ou rumor. As hashtags são **sugestões de tema**, não comprovação de tendência atual.

## Limitações honestas

1. Se a manchete não mencionar GTA, Vice City ou Grand Theft Auto, o feed pode não detectá-la, mesmo que um trecho trate de GTA.
2. RSS do YouTube exibe um número limitado de vídeos recentes. Não serve para recuperar o catálogo inteiro.
3. GitHub Actions pode atrasar ou omitir tarefas agendadas; não garante a execução exata da hora.
4. O download automático pode falhar por restrição de acesso, indisponibilidade ou direitos autorais; isso **não** desbloqueia o YouTube.
5. Artifacts não são permanentes e o GitHub não é um serviço ilimitado de armazenamento de vídeo.
6. Exibir imagens e vozes de criadores de terceiros sem autorização pode violar seus direitos.

## Fontes

- [GitHub: Actions em repositórios públicos](https://docs.github.com/en/billing/concepts/product-billing/github-actions)
- [Flow Games](https://www.youtube.com/@FlowGamesPodcast)
- [Cortes do Flow Games](https://www.youtube.com/@cortesdoflowgames)
- [GameplayRJ / Davy Jones](https://www.youtube.com/@Gameplayrj)
- [FFmpeg](https://ffmpeg.org/)
- [yt-dlp](https://github.com/yt-dlp/yt-dlp)
- [faster-whisper](https://github.com/SYSTRAN/faster-whisper)
