{
  "name": "My workflow 2",
  "nodes": [
    {
      "parameters": {
        "rule": {
          "interval": [
            {
              "triggerAtHour": 7
            }
          ]
        }
      },
      "type": "n8n-nodes-base.scheduleTrigger",
      "typeVersion": 1.2,
      "position": [
        -64,
        -160
      ],
      "id": "d4c7fd03-7f10-4cbb-9ab0-914e6eab1ff3",
      "name": "Schedule Trigger"
    },
    {
      "parameters": {
        "promptType": "define",
        "text": "ROL: Sen, konusunda uzmanlaşmış, son derece dikkatli ve analitik bir Kıdemli Pazarlama Analisti'sin. Yanıtlarında Profesyonel, Veriye Dayalı ve Özlü bir dil kullanmalısın.\n\nGÖREV: Amacın, sağlanan Tablolu CSV Metni'ni analiz etmek ve aşağıdaki adımları izleyerek bir Pazar Trend Raporu oluşturmaktır:\n1. Anahtar metrikleri (Tıklama Oranı, Dönüşüm Oranı) belirle ve veriyi temizle.\n2. Trendleri ve anormallikleri (önceki aya göre %15'ten fazla değişim) tespit et.\n3. Bulgulara dayanarak üç adet eyleme dönüştürülebilir öneri sun.\n\nGİRDİ: Aşağıdaki formatta sağlanacak olan veri/metin:\n* Tür: Tablolu CSV Metni\n* Kaynak: Son 30 günlük web sitesi trafiği verileri\n* Örnek: Tarih, Gösterim, Tıklama, Dönüşüm Sütunları\n\nARAÇLAR: Görevini yerine getirmek için aşağıdaki araçları kullanabilirsin:\n1. Google Arama: Yalnızca sektörel kıyaslama (benchmark) verilerini doğrulamak için kullan.\n2. Kod Yorumlayıcı: Yüksek hassasiyet gerektiren matematiksel hesaplamalar ve anomali tespiti için kullan.\nKullanım Notu: Araçları yalnızca görevin tamamlanması için kesinlikle gerekli olduğunda kullan.\n\nKISITLAR: Yanıtın şu kurallara kesinlikle uymalıdır:\n* Cevabın toplam uzunluğu 500 kelimeyi geçmemelidir.\n* Öznel görüş ve varsayımlar sunmaktan kaçın.\n* Tüm bulgular ve öneriler, sağlanan GİRDİ'den gelen verilerle desteklenmelidir.\n\nÇIKTI: Sonuç, yalnızca aşağıdaki Markdown formatında sunulmalıdır:\n## Pazar Trend Analizi Raporu\n\n### 📊 Ana Bulgular\n* **[Bulgu 1]**\n* **[Bulgu 2]**\n\n### 💡 Eyleme Dönük Öneriler\n\n| Öncelik | Öneri | Tahmini Etki |\n| :---: | :--- | :---: |\n| Yüksek | [Öneri 1] | Yüksek |\n| Orta | [Öneri 2] | Orta |\n\n### ⚠️ Sonuç ve Kısıtlar\n[Kısıtlara ve sonraki adımlara dair kısa bir not.]",
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.agent",
      "typeVersion": 3,
      "position": [
        208,
        0
      ],
      "id": "7a8778cc-70af-485d-9e50-6017d3b3fe38",
      "name": "AI Agent"
    },
    {
      "parameters": {
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.lmChatGoogleGemini",
      "typeVersion": 1,
      "position": [
        80,
        208
      ],
      "id": "1ff33ff8-214b-447d-8e49-0a9f8bc6e0ec",
      "name": "Google Gemini Chat Model",
      "credentials": {
        "googlePalmApi": {
          "id": "abXSItVryTMrirty",
          "name": "Google Gemini(PaLM) Api account"
        }
      }
    },
    {
      "parameters": {},
      "type": "@n8n/n8n-nodes-langchain.memoryBufferWindow",
      "typeVersion": 1.3,
      "position": [
        288,
        256
      ],
      "id": "daa4af74-a1ac-404c-965d-5c160e7de6a5",
      "name": "Simple Memory"
    },
    {
      "parameters": {
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.chatTrigger",
      "typeVersion": 1.3,
      "position": [
        -64,
        0
      ],
      "id": "5dc181ef-b37e-411e-ae94-19e69480e6f1",
      "name": "When chat message received",
      "webhookId": "167bd180-07a9-4fda-b067-ecbc0af89bfd"
    },
    {
      "parameters": {
        "operation": "getAll",
        "calendar": {
          "__rl": true,
          "mode": "list",
          "value": ""
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleCalendarTool",
      "typeVersion": 1.3,
      "position": [
        416,
        240
      ],
      "id": "727bbf2b-2834-4fd3-a21f-b283d6afa77f",
      "name": "Get many events in Google Calendar",
      "credentials": {
        "googleCalendarOAuth2Api": {
          "id": "J50Lut24p1vKcben",
          "name": "Google Calendar account 2"
        }
      }
    },
    {
      "parameters": {
        "documentId": {
          "__rl": true,
          "mode": "list",
          "value": ""
        },
        "sheetName": {
          "__rl": true,
          "mode": "list",
          "value": ""
        }
      },
      "type": "n8n-nodes-base.googleSheetsTool",
      "typeVersion": 4.7,
      "position": [
        544,
        192
      ],
      "id": "5a7b8c1d-1c5d-4737-a97d-32a4c8cc7ff1",
      "name": "Get row(s) in sheet in Google Sheets",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "VXcLtlzilGH6KAuw",
          "name": "Google Sheets account"
        }
      }
    },
    {
      "parameters": {
        "url": "https://newsdata.io/api/1/latest?apikey=YOUR_API_KEY",
        "options": {}
      },
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.3,
      "position": [
        720,
        192
      ],
      "id": "f50f45a7-88c5-4caa-9e5c-46e13d553a90",
      "name": "HTTP Request"
    },
    {
      "parameters": {
        "sendTo": "caniksemih54@gmail.com",
        "subject": "={{ /*n8n-auto-generated-fromAI-override*/ $fromAI('Subject', ``, 'string') }}",
        "message": "={{ /*n8n-auto-generated-fromAI-override*/ $fromAI('Message', ``, 'string') }}",
        "options": {}
      },
      "type": "n8n-nodes-base.gmailTool",
      "typeVersion": 2.1,
      "position": [
        672,
        400
      ],
      "id": "0c958465-ef41-4ec3-90df-36833dfc4b49",
      "name": "Send a message in Gmail",
      "webhookId": "3eee65b5-e49c-4218-bbf4-1f1a6337a090",
      "credentials": {
        "gmailOAuth2": {
          "id": "iU7dzSpvdWppcfOC",
          "name": "Gmail account"
        }
      }
    }
  ],
  "pinData": {},
  "connections": {
    "Schedule Trigger": {
      "main": [
        []
      ]
    },
    "Google Gemini Chat Model": {
      "ai_languageModel": [
        [
          {
            "node": "AI Agent",
            "type": "ai_languageModel",
            "index": 0
          }
        ]
      ]
    },
    "Simple Memory": {
      "ai_memory": [
        [
          {
            "node": "AI Agent",
            "type": "ai_memory",
            "index": 0
          }
        ]
      ]
    },
    "When chat message received": {
      "main": [
        [
          {
            "node": "AI Agent",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Get many events in Google Calendar": {
      "ai_tool": [
        [
          {
            "node": "AI Agent",
            "type": "ai_tool",
            "index": 0
          }
        ]
      ]
    },
    "Get row(s) in sheet in Google Sheets": {
      "ai_tool": [
        [
          {
            "node": "AI Agent",
            "type": "ai_tool",
            "index": 0
          }
        ]
      ]
    }
  },
  "active": false,
  "settings": {
    "executionOrder": "v1"
  },
  "versionId": "dd3ca2bb-f85d-4762-bd40-a6a372dbd72b",
  "meta": {
    "templateCredsSetupCompleted": true,
    "instanceId": "7ff76dad8992a19e29bbdd6b7fc62bfaf70a9341c3be8ad3e9a24b52728d7415"
  },
  "id": "kgDHVrY7NBS1o4UV",
  "tags": []
}
