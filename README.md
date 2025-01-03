# Cutie-Grabber
# List of actresses (add as many as you like)
actresses = [
    "Scarlett Johansson",
    "Emma Watson",
    "Jennifer Lawrence",
    "Natalie Portman",
    "Margot Robbie",
    "Angelina Jolie",
    "Anne Hathaway",
]

# Current random actress
current_actress = None

# Start command
def start(update: Update, context: CallbackContext):
    update.message.reply_text("Welcome to the Actress Guessing Game Bot!")
    update.message.reply_text("Type /new to get a new actress or /guess <name> to make a guess!")

# Send a new random actress
def new_actress(update: Update, context: CallbackContext):
    global current_actress
    current_actress = random.choice(actresses)
    update.message.reply_text("Guess the name of the actress!")

# Guess command
def guess(update: Update, context: CallbackContext):
    global current_actress
    if not current_actress:
        update.message.reply_text("Start a new round with /new first!")
        return
    
    user_guess = " ".join(context.args)
    if user_guess.lower() == current_actress.lower():
        update.message.reply_text(f"Correct! The actress was {current_actress}. Type /new to play again!")
        current_actress = None
    else:
        update.message.reply_text("Incorrect! Try again!")

# Main function to run the bot
def main():
    # Replace 'YOUR_BOT_TOKEN' with your actual bot token
    updater = Updater("YOUR_BOT_TOKEN")
    dispatcher = updater.dispatcher

    # Command handlers
    dispatcher.add_handler(CommandHandler("start", start))
    dispatcher.add_handler(CommandHandler("new", new_actress))
    dispatcher.add_handler(CommandHandler("guess", guess))

    # Start the bot
    updater.start_polling()
    updater.idle()

if name == "main":
    main()
