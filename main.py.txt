from telegram import Bot, Update, InlineKeyboardButton, InlineKeyboardMarkup, InputMediaPhoto
from telegram.ext import Application, CommandHandler, CallbackQueryHandler, CallbackContext

# 🔹 Bot API Token
TOKEN = "8143911604:AAG5FLxevOPQol3EF7qMxy20mcroIF0awxI"

# 🔹 Bot Setup
app = Application.builder().token(TOKEN).build()

# 🔹 Start Command Function
async def start(update: Update, context: CallbackContext):
    chat_id = update.message.chat_id

    keyboard = [[InlineKeyboardButton("♻️ Condition", callback_data="condition_pressed")]]
    reply_markup = InlineKeyboardMarkup(keyboard)

    await context.bot.send_photo(
        chat_id=chat_id,
        photo="https://i.postimg.cc/V6CnKhGL/In-Shot-20250129-064912963.jpg",
        caption=(
            "Welcome to Gambling Jackpot Bot 🎰\n\n"
            "The bot is powered by OpenAI neural network system 🖥[ChatGPT-v4].\n\n"
            "For training, the bot played 🎰 more than 8000 games.\n"
            "Currently, bot users successfully earn 20-30% of their 💵 capital each day!\n\n"
            "The bot is still improving, and its accuracy stands at 90%! 🚀\n\n"
            "To gain access, certain conditions must be met👇"
        ),
        reply_markup=reply_markup
    )

# 🔹 Condition Button Click Event (Old Post Hide, New Post Show)
async def condition_callback(update: Update, context: CallbackContext):
    query = update.callback_query

    keyboard = [
        [InlineKeyboardButton("📲 REGISTER", url="https://1whfbb.life/?open=register&p=lx6n")],
        [InlineKeyboardButton("🔍 CHECK REGISTRATION", callback_data="check_registration")]
    ]
    reply_markup = InlineKeyboardMarkup(keyboard)

    await query.edit_message_media(
        media=InputMediaPhoto(
            media="https://i.postimg.cc/Bvx1DFXX/10-GEM-4.jpg",
            caption=(
                "🌐 Step 1 - Register\n\n"
                "‼️ The account must be new.\n\n"
                "1️⃣ If you are directed to an existing account after clicking the 'REGISTER' button, please log out and click the button again.\n\n"
                "2️⃣ Don't forget to enter the promo code 10GEM 🎁 during registration.\n\n"
                "✅ Once you have completed your REGISTRATION, click the 'CHECK REGISTRATION' button."
            ),
            parse_mode="Markdown"
        ),
        reply_markup=reply_markup
    )

# 🔹 Check Registration Button Click Event
async def check_registration_callback(update: Update, context: CallbackContext):
    query = update.callback_query
    await query.answer(text="❌ Register not found ❌", show_alert=True)

# 🔹 Bot Run Function
def main():
    app.add_handler(CommandHandler("start", start))
    app.add_handler(CallbackQueryHandler(condition_callback, pattern="condition_pressed"))
    app.add_handler(CallbackQueryHandler(check_registration_callback, pattern="check_registration"))

    print("🤖 Bot is running...")
    app.run_polling()

# 🔹 Run Bot
if __name__ == "__main__":
    main()

