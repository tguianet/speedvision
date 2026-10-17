# SpeedVision Tennis — módulo de análise de partidas

## Objetivo
Aplicativo Android/iOS que grava partidas de tênis e, após a gravação, analisa a trajetória da bola, rebatidas e jogadores. O SpeedVision original de velocidade de atletas permanece independente.

## Fluxo do MVP
1. Capturar ou importar vídeo horizontal (preferência 1080p/60 fps), com celular fixo atrás da linha de fundo.
2. Cadastrar partida e jogadores (lado próximo e distante).
3. Calibrar manualmente os quatro cantos e as linhas visíveis da quadra.
4. Processar quadros e localizar bola e jogadores; associar detecções entre quadros.
5. Desenhar trajetória com lacunas quando a bola estiver oculta; permitir replay.
6. Identificar candidatos a rebatidas e quiques com grau de confiança e revisão manual.
7. Exibir contagens por jogador apenas para eventos confirmados.

## Fases de análise
- Fase 1: gravação/importação, biblioteca, replay, calibração e rastro da bola.
- Fase 2: identidade dos jogadores, rebatidas, forehand, backhand e saque.
- Fase 3: classificação dentro/fora e velocidade estimada, com métricas de erro validadas.

## Arquitetura proposta
- Mobile: React Native + Expo (Android/iOS).
- API: Python + FastAPI, processamento assíncrono.
- Visão: OpenCV e detector de bola treinado para objetos pequenos, rastreamento temporal; detecção de jogadores e pose.
- Dados: partidas, jogadores, vídeos, calibrações, eventos, confiança e revisões.
- Vídeos: armazenamento privado com retenção configurável.

## Regras de qualidade
- Nunca classificar bola dentro/fora sem quique e geometria confiáveis.
- Mostrar 'inconclusivo' quando houver oclusão, borrão ou baixa resolução.
- Contagem de golpes deve distinguir jogador e contato provável; permitir correção manual.
- Não prometer precisão Hawk-Eye com uma única câmera.
- Testar com vídeos reais e métricas de precisão, recall e erro de localização.

## Próximo passo de implementação
Criar projeto Expo dentro de `tennis/mobile`, serviço FastAPI em `tennis/api` e testes com um vídeo de 30–60 segundos.
