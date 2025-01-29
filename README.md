# 🌟 Aisyah AI 🌟

![Avatar](https://github.com/husniadil/aisyah-ai/blob/main/assets/avatar.jpg?raw=true)

Aisyah AI is a multi-functional project that provides various tools and capabilities for interacting with users, setting reminders, processing images, and making web requests. It leverages Cloudflare Workers for serverless functions, utilizing APIs from OpenAI for language processing and image recognition, as well as real-time weather data and Telegram for message handling.

## Features

- **🗣️ Natural Language Processing**: 
  - **Understanding Queries**: Aisyah AI can comprehend natural language inputs, making it easy for users to ask questions in plain English.
  - **Conversational Responses**: It provides conversational responses, making interactions feel more human-like and engaging.

- **🖼️ Image Recognition**: 
  - **Image Analysis**: Aisyah AI can analyze images to identify objects, people, and scenes.
  - **Information Extraction**: It can provide detailed information about the contents of an image, such as identifying landmarks or categorizing items.

- **🌤️ Weather Forecast**: 
  - **Real-time Data**: Aisyah AI provides up-to-date weather information for any specified location.

- **⏰ Reminder Service**: 
  - **Setting Reminders**: Users can set reminders for various tasks and events.
  - **Notifications**: Aisyah AI sends timely notifications to remind users of their scheduled tasks.

- **🌐 Web Requests**: 
  - **Data Retrieval**: Aisyah AI can perform web requests to fetch information from various online sources.
  - **Processing Results**: The AI processes and presents the retrieved data in a user-friendly format.

- **📲 Telegram Integration**: 
  - **Seamless Messaging**: Aisyah AI interacts with users via Telegram, providing a smooth and efficient messaging experience.
  - **Real-time Interaction**: The integration allows for real-time communication and quick responses.

- **☁️ Serverless Functions**: 
  - **Scalability**: Leveraging Cloudflare Workers ensures that Aisyah AI can scale efficiently to handle increasing workloads.
  - **Reliability**: Serverless architecture provides high availability and reliability, minimizing downtime.
  - **Cost-effective**: Serverless functions help in reducing operational costs by only charging for actual usage.

- **🔗 API Integration**: 
  - **Advanced Capabilities**: By integrating with various APIs, Aisyah AI can offer advanced functionalities beyond basic responses.
  - **Third-party Services**: It connects with third-party services to enhance its capabilities, such as language translation, sentiment analysis, and more.
  - **Continuous Improvement**: Regular updates and new API integrations keep Aisyah AI up-to-date with the latest technological advancements.

## Screenshots

[<img src="https://github.com/husniadil/aisyah-ai/blob/main/assets/start-1.png?raw=true" width="200" alt="start-1" />](https://github.com/husniadil/aisyah-ai/blob/main/assets/start-1.png)
[<img src="https://github.com/husniadil/aisyah-ai/blob/main/assets/start-2.png?raw=true" width="200" alt="start-2" />](https://github.com/husniadil/aisyah-ai/blob/main/assets/start-2.png)
[<img src="https://github.com/husniadil/aisyah-ai/blob/main/assets/settings-llm-model.png?raw=true" width="200" alt="settings-llm-model" />](https://github.com/husniadil/aisyah-ai/blob/main/assets/settings-llm-model.png)
[<img src="https://github.com/husniadil/aisyah-ai/blob/main/assets/settings-persona.png?raw=true" width="200" alt="settings-persona" />](https://github.com/husniadil/aisyah-ai/blob/main/assets/settings-persona.png)
[<img src="https://github.com/husniadil/aisyah-ai/blob/main/assets/settings-voice.png?raw=true" width="200" alt="settings-voice" />](https://github.com/husniadil/aisyah-ai/blob/main/assets/settings-voice.png)
[<img src="https://github.com/husniadil/aisyah-ai/blob/main/assets/settings-chat-history.png?raw=true" width="200" alt="settings-chat-history" />](https://github.com/husniadil/aisyah-ai/blob/main/assets/settings-chat-history.png)
[<img src="https://github.com/husniadil/aisyah-ai/blob/main/assets/chat.png?raw=true" width="200" alt="chat" />](https://github.com/husniadil/aisyah-ai/blob/main/assets/chat.png)
[<img src="https://github.com/husniadil/aisyah-ai/blob/main/assets/group-chat.png?raw=true" width="200" alt="group-chat" />](https://github.com/husniadil/aisyah-ai/blob/main/assets/group-chat.png)

## Usage

**Personal Use Only**: Please note that Aisyah AI is a personal project and not intended for production use. It is designed for personal experimentation and learning purposes.

- **Experimentation**: Users can experiment with different features and functionalities to learn more about AI and serverless technologies.
- **Learning**: Aisyah AI serves as an educational tool for those interested in understanding how AI and serverless functions work.
- **Customization**: Users can customize Aisyah AI for their personal needs, adding new features or modifying existing ones.

## Setup

### Wrangler Configuration

Before running the project, you need to set up the wrangler configuration files:

1. Set up Cloudflare API Token:
   - Go to https://dash.cloudflare.com/profile/api-tokens
   - Locate "Edit Cloudflare Workers", then "Use Template"
   - Fill out the rules
   - Click "Continue to summary"
   - Export the token as an environment variable:
     ```bash
     export CLOUDFLARE_API_TOKEN=your_api_token_here
     ```
   - For persistent configuration, add it to your shell profile (~/.zshrc, ~/.bashrc, etc.):
     ```bash
     echo 'export CLOUDFLARE_API_TOKEN=your_api_token_here' >> ~/.zshrc
     ```

2. Copy the example configuration files:
   ```bash
   cp packages/aisyah-ai-agent/wrangler.toml.example packages/aisyah-ai-agent/wrangler.toml
   cp packages/aisyah-ai-explorer/wrangler.toml.example packages/aisyah-ai-explorer/wrangler.toml
   cp packages/aisyah-ai-reminder/wrangler.toml.example packages/aisyah-ai-reminder/wrangler.toml
   cp packages/aisyah-ai-sonata/wrangler.toml.example packages/aisyah-ai-sonata/wrangler.toml
   cp packages/aisyah-ai-storm/wrangler.toml.example packages/aisyah-ai-storm/wrangler.toml
   cp packages/aisyah-ai-telegraph/wrangler.toml.example packages/aisyah-ai-telegraph/wrangler.toml
   cp packages/aisyah-ai-vision/wrangler.toml.example packages/aisyah-ai-vision/wrangler.toml
   cp packages/aisyah-ai-whisper/wrangler.toml.example packages/aisyah-ai-whisper/wrangler.toml
   ```

3. Update the configuration files with your actual values:
   - In `packages/aisyah-ai-agent/wrangler.toml`:
     - Replace `<YOUR_KV_NAMESPACE_ID>` with your KV namespace ID
   - In `packages/aisyah-ai-sonata/wrangler.toml`:
     - Replace `<YOUR_SUPABASE_STORAGE_KEY>` with your Supabase storage key
     - Replace `<YOUR_KV_NAMESPACE_ID>` with your KV namespace ID

4. Create KV namespaces if you haven't:
   ```bash
   wrangler kv:namespace create SETTINGS
   ```

Note: The actual wrangler.toml files are gitignored to prevent committing sensitive information.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
