# bot-discord
import discord
from bot_logic import gen_pass
import random
from settings import settings
# import * - è un modo rapido per importare tutti i file della libreria.
from bot_logic import *

# La variabile intents memorizza i privilegi del bot
intents = discord.Intents.default()
# Abilitazione del privilegio di lettura dei messaggi
intents.message_content = True
# Creare un bot nella variabile client e trasferirgli i privilegi
client = discord.Client(intents=intents)


# Una volta che il bot è pronto, stamperà il suo nome!
@client.event
async def on_ready():
    print('Abbiamo effettuato laccesso come" {client.user}')


# Quando il bot riceve un messaggio, invia messaggi nello stesso canale!
@client.event
async def on_message(message):
    if message.author == client.user:
        return
    if message.content.startswith('$hello'):
        await message.channel.send('Ciao! Sono un bot!')
    elif message.content.startswith('$smile'):
        await message.channel.send(gen_emodji())
    elif message.content.startswith('$coin'):
        await message.channel.send(flip_coin())
    elif message.content.startswith('$pass'):
        await message.channel.send(gen_pass(10))
    else:
        await message.channel.send("Non è possibile elaborare questo comando, mi dispiace!")

client.run(settings["TOKEN"])

# la variabile intents contiene i permessi al bot
intents = discord.Intents.default()
# abilita il permesso a leggere i contenuti dei messaggi
intents.message_content = True
# crea un bot e passa gli indents
client = discord.Client(intents=intents)

@client.event
async def on_ready():
    print(f'Abbiamo fatto l\'accesso come {client.user}')

@client.event
async def on_message(message):
    if message.author == client.user:
        return
    if message.content.startswith('$ciao'):
        await message.channel.send("Ciao!")
    elif message.content.startswith('$arrivederci'):
        await message.channel.send("\U0001f642")
    else:
        await message.channel.send(message.content)


@client.event

def gen_pass(pass_length):
    elements = "+-/*!&$#?=@<>"
    password = ""
    async def on_message(message):
        if message.content.startswith('creami una password'):
            for i in range(pass_length):
                password += random.choice(elements)
            gen_pass(10)
            return password
        print(pass_length)

@client.event
def gen_emodji():
    async def on_message(message):
        if message.content.startswith('scrivimi una emoji'):
            emoji = ["\U0001f600", "\U0001f642", "\U0001F606", "\U0001F923"]
            return random.choice(emoji)
        print(emoji)

@client.event
def flip_coin():
    async def on_message(message):
        if message.content.startswith('testa o croce'):
            flip = random.randint(0, 2)
        if flip == 0:
            return print("HEADS")
        else:
            return print("TAILS")
        
client.run("MTMxMjA5NDA4NTUyNzM3NTk4NA.G2srDu.Eezb5dXvkgI9gA22SiOCIcSYXN0n1-FQ9d65qg")
