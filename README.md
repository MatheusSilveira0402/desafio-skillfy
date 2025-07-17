# Desafio Técnico - App de Gerenciamento de Tarefas 📱✅

Este desafio foi criado para avaliar suas habilidades em desenvolvimento mobile com Flutter, consumo de APIs e criação de interfaces modernas.

## 🎯 Objetivo

Desenvolver uma aplicação mobile usando Flutter que permita aos usuários gerenciar suas tarefas diárias, com integração a uma API de produtividade que sugere o melhor horário para realizar cada tarefa.

## 📋 Pré-requisitos

- Conhecimento em:
  - Flutter & Dart
  - Consumo de APIs REST
  - Gerenciamento de estado (Provider, Riverpod ou Bloc)
  - UI/UX
  - Git

## 🧩 O que você deve fazer

1. Criar uma aplicação mobile usando Flutter

2. Implementar as seguintes funcionalidades:
   - Dashboard com visão geral das tarefas
   - Lista de tarefas com filtros e ordenação
   - Formulário de criação/edição de tarefas
   - Integração com a API de produtividade

3. Consumir a API de produtividade:
   - Endpoint: `/suggest-time`
   - Método: POST
   - Payload:
     ```json
     {
       "task": {
         "title": "Reunião com equipe",
         "priority": "high",
         "estimated_duration": 60,
         "deadline": "2024-03-20T15:00:00Z",
         "category": "work"
       },
       "user_preferences": {
         "working_hours": {
           "start": "09:00",
           "end": "18:00"
         },
         "preferred_categories": ["work", "personal"]
       }
     }
     ```

4. Implementar uma interface moderna e responsiva:
   - Material Design 3 (Material You)
   - Animações suaves usando Flutter animations
   - Feedback visual para ações do usuário
   - Tratamento de estados de loading e erro

## 📁 Estrutura do Projeto

```
.
├── lib/
│   ├── main.dart
│   ├── app.dart
│   ├── models/
│   │   ├── task.dart
│   │   ├── task_suggestion.dart
│   │   └── user_preferences.dart
│   ├── screens/
│   │   ├── dashboard/
│   │   │   └── dashboard_screen.dart
│   │   ├── task_list/
│   │   │   └── task_list_screen.dart
│   │   └── task_form/
│   │       └── task_form_screen.dart
│   ├── widgets/
│   │   ├── task_card.dart
│   │   ├── priority_badge.dart
│   │   ├── category_filter.dart
│   │   └── time_suggestions.dart
│   ├── services/
│   │   ├── api_service.dart
│   │   └── task_service.dart
│   ├── providers/
│   │   ├── task_provider.dart
│   │   └── theme_provider.dart
│   ├── utils/
│   │   ├── constants.dart
│   │   └── helpers.dart
│   └── theme/
│       ├── app_theme.dart
│       └── app_colors.dart
├── android/
├── ios/
├── test/
├── pubspec.yaml
└── README.md
```

## 🎨 Design

### Cores
- Primária: #6366F1 (Indigo)
- Secundária: #10B981 (Emerald)
- Fundo: #F9FAFB
- Texto: #1F2937

### Tipografia
- Fonte principal: Inter
- Tamanhos: 12px - 24px
- Pesos: Regular (400), Medium (500), Bold (700)

## 📱 Telas

### 1. Dashboard
- Resumo do dia
- Tarefas prioritárias
- Gráfico de produtividade
- Sugestões de horários

### 2. Lista de Tarefas
- Cards de tarefas com:
  - Título
  - Prioridade
  - Categoria
  - Horário sugerido
  - Status
- Filtros por:
  - Categoria
  - Prioridade
  - Status
- Ordenação por:
  - Data
  - Prioridade
  - Nome

### 3. Formulário de Tarefa
- Campos:
  - Título
  - Descrição
  - Categoria
  - Prioridade
  - Duração estimada
  - Prazo
  - Lembretes
- Sugestões de horário
- Preview da tarefa

## 🔧 Considerações Técnicas

### Simulação da API

Para desenvolvimento, você pode simular a API usando o JSON Server. Siga os passos abaixo:

1. Instale o JSON Server:
```bash
npm install -g json-server
```

2. Crie um arquivo `db.json` na raiz do projeto:
```json
{
  "tasks": [
    {
      "id": 1,
      "title": "Reunião com equipe",
      "description": "Discussão sobre o novo projeto",
      "priority": "high",
      "category": "work",
      "estimated_duration": 60,
      "deadline": "2024-03-20T15:00:00Z",
      "status": "pending"
    }
  ],
  "suggestions": [
    {
      "task_id": 1,
      "suggested_times": [
        {
          "start": "2024-03-20T10:00:00Z",
          "end": "2024-03-20T11:00:00Z",
          "score": 0.9
        },
        {
          "start": "2024-03-20T14:00:00Z",
          "end": "2024-03-20T15:00:00Z",
          "score": 0.8
        }
      ]
    }
  ]
}
```

3. Inicie o servidor:
```bash
json-server --watch db.json --port 3001
```

4. Endpoints disponíveis:
- `GET /tasks` - Lista todas as tarefas
- `GET /tasks/:id` - Obtém uma tarefa específica
- `POST /tasks` - Cria uma nova tarefa
- `PUT /tasks/:id` - Atualiza uma tarefa
- `DELETE /tasks/:id` - Remove uma tarefa
- `POST /suggest-time` - Simula a sugestão de horário

5. Exemplo de uso da API de sugestão de horário:
```dart
// services/api_service.dart
import 'dart:convert';
import 'package:http/http.dart' as http;

class ApiService {
  static const String _baseUrl = 'http://localhost:3001';

  static Future<Map<String, dynamic>> suggestTime(Map<String, dynamic> taskData) async {
    final response = await http.post(
      Uri.parse('$_baseUrl/suggest-time'),
      headers: {
        'Content-Type': 'application/json',
      },
      body: jsonEncode(taskData),
    );
    
    if (response.statusCode == 200) {
      return jsonDecode(response.body);
    } else {
      throw Exception('Failed to get time suggestions');
    }
  }
}
```

6. Para simular diferentes cenários, você pode modificar o `db.json` com diferentes dados de teste.

### Versões Recomendadas
- Flutter 3.27+
- Dart 3.8+
- Material Design 3
- Provider, Riverpod ou Bloc para gerenciamento de estado
- http ou dio para requisições HTTP
- shared_preferences para persistência local
- flutter_test para testes unitários

### Dependências Sugeridas
```yaml
dependencies:
  flutter:
    sdk: flutter
  http: ^1.1.0
  provider: ^6.1.1  # ou riverpod/bloc
  shared_preferences: ^2.2.2
  intl: ^0.18.1
  flutter_svg: ^2.0.9

dev_dependencies:
  flutter_test:
    sdk: flutter
  flutter_lints: ^3.0.0
  mockito: ^5.4.4
```

### Performance
- Lazy loading de widgets
- Uso eficiente de setState
- Implementação de paginação para listas grandes
- Cache de requisições HTTP
- Otimização de imagens e assets

### Acessibilidade
- Uso adequado de Semantics widgets
- Suporte a leitores de tela
- Contraste adequado de cores
- Tamanhos de toque apropriados
- Suporte a modo escuro

## 🚀 Como entregar

1. Faça um **fork** deste repositório
2. Realize o desafio no seu fork
3. Ao finalizar, envie um **Pull Request** para este repositório com a sua solução

### 📱 Entrega do APK

Além do código fonte, você deve gerar um APK de release:

1. Gerar um APK de release:
   ```bash
   flutter build apk --release
   ```

2. O APK gerado estará localizado em: `build/app/outputs/flutter-apk/app-release.apk`

3. Adicione o APK ao repositório em uma pasta chamada `release/`

4. Inclua no README:
   - Link para download do APK
   - Versão mínima do Android suportada (recomendado: API 21+)
   - Permissões necessárias
   - Instruções de instalação
   - Screenshots da aplicação

### Exemplo de seção no README para o APK:
```markdown
## 📱 Download do APK

- **APK Release**: [Download aqui](./release/app-release.apk)
- **Versão mínima do Android**: API 21 (Android 5.0)
- **Tamanho**: ~XX MB
- **Permissões**: Internet

### Como instalar:
1. Baixe o arquivo APK
2. Ative "Fontes desconhecidas" nas configurações do Android
3. Toque no arquivo APK e siga as instruções de instalação
```

## ✅ Critérios de Avaliação

- Qualidade do código Dart e organização
- Uso adequado dos widgets Flutter
- Fidelidade ao Material Design 3
- Experiência do usuário mobile
- Tratamento de erros e estados de loading
- Performance e otimizações
- Testes implementados
- Gerenciamento de estado eficiente
- Documentação do projeto
- Implementação de funcionalidades extras (diferencial)

---

Boa sorte e divirta-se desenvolvendo! 🚀

## 📚 Referências

- [Flutter Documentation](https://flutter.dev/docs)
- [Dart Documentation](https://dart.dev/guides)
- [Material Design 3](https://m3.material.io/)
- [Provider Documentation](https://pub.dev/packages/provider)
- [Riverpod Documentation](https://riverpod.dev/)
- [Bloc Documentation](https://bloclibrary.dev/)
- [HTTP Package Documentation](https://pub.dev/packages/http)
- [Flutter Testing Documentation](https://flutter.dev/docs/testing)
- [Material Design Guidelines](https://material.io/design)
- [Flutter Performance Best Practices](https://flutter.dev/docs/perf/best-practices) 