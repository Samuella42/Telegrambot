from telegram import Update
from telegram.ext import Updater, CommandHandler, MessageHandler, Filters, CallbackContext
import random

# Bot token'ını buraya girin
TOKEN = '6720502314:AAEgcAcBoeJLWgoGjMp80By3OCb9iSWYpSU'

# Oyun durumu için global değişkenler
game_state = {}

def start(update: Update, context: CallbackContext) -> None:
    update.message.reply_text('Merhaba! Sayı Tahmin Oyunu için /oyun komutunu kullanın.')

def start_game(update: Update, context: CallbackContext) -> None:
    user_id = update.message.from_user.id
    game_state[user_id] = {'number': random.randint(1, 100), 'attempts': 0}
    update.message.reply_text('1 ile 100 arasında bir sayı tahmin et. Başarılar!')

def guess(update: Update, context: CallbackContext) -> None:
    user_id = update.message.from_user.id
    if user_id not in game_state:
        update.message.reply_text('Önce /oyun komutunu kullanarak oyunu başlatın.')
        return

    try:
        user_guess = int(update.message.text)
        game_state[user_id]['attempts'] += 1

        if user_guess < game_state[user_id]['number']:
            update.message.reply_text('Daha yüksek bir sayı deneyin.')
        elif user_guess > game_state[user_id]['number']:
            update.message.reply_text('Daha düşük bir sayı deneyin.')
        else:
            update.message.reply_text(f'Tebrikler! {game_state[user_id]["attempts"]} denemede buldunuz.')
            del game_state[user_id]
    except ValueError:
        update.message.reply_text('Lütfen geçerli bir sayı girin.')

def main() -> None:
    updater = Updater(TOKEN)

    dispatcher = updater.dispatcher

    dispatcher.add_handler(CommandHandler('start', start))
    dispatcher.add_handler(CommandHandler('oyun', start_game))
    dispatcher.add_handler(MessageHandler(Filters.text & ~Filters.command, guess))

    updater.start_polling()

    updater.idle()

if __name__ == '__main__':
    main()
