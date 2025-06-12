import discord
from discord.ext import commands
import random

intents = discord.Intents.default()
intents.message_content = True

# Configuración básica
bot = commands.Bot(command_prefix='#', intents=discord.Intents.default())

# Datos ecológicos
reciclaje_info = {
    "biologia": (
        "🌿 **Biología y Ecología**\n"
        "La biología estudia:\n"
        "- Seres vivos y sus interacciones\n"
        "- Ecosistemas y biodiversidad\n"
        "- Impacto humano en la naturaleza\n\n"
        "🔬 Aplicaciones:\n"
        "- Conservación de especies\n"
        "- Biorremediación de suelos\n"
        "- Estudios climáticos"
    ),
    "fenomenos": [
        "🌪️ **Huracanes**:\n"
        "Causados por calentamiento oceánico\n"
        "Soluciones:\n"
        "- Reducir emisiones\n"
        "- Proteger manglares",

        "🔥 **Incendios**:\n"
        "Prevención:\n"
        "- Franjas cortafuegos\n"
        "- Monitoreo satelital",

        "🌊 **Inundaciones**:\n"
        "Medidas:\n"
        "- Reforestación\n"
        "- Sistemas de drenaje"
    ],
    "contaminacion": (
        "🚗 **Contaminación vehicular**\n"
        "Problemas:\n"
        "- Gases efecto invernadero\n"
        "- Daño a la capa de ozono\n\n"
        "💡 Soluciones:\n"
        "- Filtros para autos\n"
        "- Transporte público eléctrico\n"
        "- Uso de bicicletas"
    ),
    "energias": (
        "⚡ **Energías renovables**\n"
        "1. Solar: Paneles fotovoltaicos\n"
        "2. Eólica: Molinos de viento\n"
        "3. Hidroeléctrica: Represas\n"
        "4. Geotérmica: Calor terrestre"
    )
}

# Consejos ecológicos prácticos
consejos_ecologicos = [
    "♻️ Usa botellas de agua reutilizables en lugar de comprar botellas de plástico",
    "🚲 Considera caminar o usar bicicleta para distancias cortas",
    "💡 Apaga las luces cuando salgas de una habitación",
    "🚰 Cierra el grifo mientras te cepillas los dientes",
    "🛒 Lleva tus propias bolsas al supermercado",
    "🌱 Planta un árbol o cuida plantas en tu hogar",
    "📱 Desconecta cargadores que no estés usando",
    "🍎 Compra productos locales y de temporada"
]

# Química sostenible
quimica_verde = [
    "🧪 Usa productos de limpieza ecológicos",
    "🚫 Evita productos con ftalatos y parabenos",
    "♻️ Recicla pilas y baterías en contenedores especiales",
    "🌍 Prefiere productos con envases biodegradables",
    "💧 Ahorra agua en tus experimentos químicos caseros"
]

# Comandos básicos
@bot.command()
async def ayuda(ctx):
    """Muestra los comandos disponibles"""
    embed = discord.Embed(
        title="🌍 Comandos EcoBot",
        description="Información científica verificada\nAsesoría: Bióloga Karla Aparicio y Química Prof.Lourdes Poveda",
        color=0x00ff00
    )
    
    embed.add_field(
        name="🔬 Ciencia Ambiental",
        value="`#biologia` - Fundamentos ecológicos\n"
              "`#fenomenos` - Fenómenos naturales\n"
              "`#contaminacion` - Soluciones ambientales\n"
              "`#energias` - Energías renovables",
        inline=False
    )
    
    embed.add_field(
        name="💡 Acciones Prácticas",
        value="`#consejo` - Consejo ecológico\n"
              "`#quimica` - Química sostenible\n"
              "`#accion` - Acción concreta para hoy",
        inline=False
    )
    
    embed.set_footer(text="¡Cada pequeña acción cuenta para nuestro planeta!")
    await ctx.send(embed=embed)

@bot.command()
async def biologia(ctx):
    """Explica la importancia de la biología en ecología"""
    await ctx.send(reciclaje_info["biologia"])

@bot.command()
async def fenomenos(ctx):
    """Información sobre fenómenos naturales"""
    await ctx.send(random.choice(reciclaje_info["fenomenos"]))

@bot.command()
async def contaminacion(ctx):
    """Soluciones para la contaminación"""
    await ctx.send(reciclaje_info["contaminacion"])

@bot.command()
async def energias(ctx):
    """Explica las energías renovables"""
    await ctx.send(reciclaje_info["energias"])

@bot.command()
async def consejo(ctx):
    """Envía un consejo ecológico práctico"""
    consejo = random.choice(consejos_ecologicos)
    await ctx.send(f"💚 **Consejo Ecológico:**\n{consejo}")

@bot.command()
async def quimica(ctx):
    """Enseña sobre química sostenible"""
    consejo_quimico = random.choice(quimica_verde)
    await ctx.send(f"🧪 **Química Verde:**\n{consejo_quimico}")

@bot.command()
async def accion(ctx):
    """Sugiere una acción concreta para ayudar"""
    acciones = [
        "🌿 Hoy puedes: Separar tus residuos en orgánicos e inorgánicos",
        "♻️ Hoy puedes: Reciclar una botella de plástico",
        "💡 Hoy puedes: Cambiar una bombilla tradicional por una LED",
        "🚰 Hoy puedes: Reducir tu tiempo de ducha en 2 minutos",
        "🛒 Hoy puedes: Comprar un producto sin empaque plástico"
    ]
    await ctx.send(random.choice(acciones))

# Eventos del bot
@bot.event
async def on_ready():
    await bot.change_presence(activity=discord.Game(name="Escribe #ayuda para información ecológica"))
    print(f'Bot listo como {bot.user.name}')

# Iniciar el bot
bot.run('TU TOKEN')  # Reemplaza con tu token real
