# Projet-d-informaimport ollama

# Nom du modèle (déjà installé avec ollama pull)
MODEL_NAME = 'deepseek-r1:7b-qwen-distill-q4_K_M'

# Instructions initiales à l'IA
system_prompt = (
    "Tu es une IA qui fait deviner des concepts abstraits en français. "
    "Tu choisis un concept abstrait (comme la liberté, la haine, la justice, etc.), "
    "sans le révéler. Tu donnes un indice à la fois pour que l'humain devine. "
    "Quand il devine, tu confirmes s’il a trouvé ou pas. "
    "Ne donne pas directement le concept à moins qu’il abandonne. "
    "Commence maintenant avec un concept et donne un premier indice."
)

# Historique de la conversation avec l'IA
conversation = [
    {"role": "system", "content": system_prompt},
]

print("\n🎭 Bienvenue dans 'Devine tête de concept abstrait avec une IA' !")
print("🧠 L’IA pense à un concept abstrait... Essaie de le deviner !")
print("✍️ Tape 'indice' pour avoir un nouvel indice.")
print("❌ Tape 'abandon' pour connaître la réponse.\n")

# Lancement initial de l'IA
response = ollama.chat(model=MODEL_NAME, messages=conversation)
print("🤖 Indice : " + response['message']['content'])
conversation.append({"role": "assistant", "content": response['message']['content']})

# Boucle principale du jeu
while True:
    user_input = input("\n💬 Ta réponse : ").strip().lower()

    if user_input == "abandon":
        conversation.append({"role": "user", "content": "J’abandonne. Dis-moi la réponse."})
        response = ollama.chat(model=MODEL_NAME, messages=conversation)
        print("🤖 Réponse : " + response['message']['content'])
        break

    elif user_input == "indice":
        conversation.append({"role": "user", "content": "Donne-moi un autre indice."})
    else:
        conversation.append({"role": "user", "content": f"Est-ce que c’est '{user_input}' ?"})
    
    response = ollama.chat(model=MODEL_NAME, messages=conversation)
    print("🤖 " + response['message']['content'])
    conversation.append({"role": "assistant", "content": response['message']['content']})tique-L1
Devinette de sujet abstrait avec une IA
