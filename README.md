We all seen "$2500 from Mr.Beast" spam message in discord, it's pretty annoying to delete it from all channels of a server, especially if it's a big server. I created a script that uses YAGPDB bot to handle these spam messages. It timeouts the user before it can spread $2500 in all of your server's channels.

# Setting up discord server
1. Create a text channel, and name it something like **anti-spam-dont-text** to warn others. Place it on top of the channel list and make sure anyone can see and write or post in it.
2. Sign in [YAGPDB](https://yagpdb.xyz) website with your discord account, make sure that account have admin powers in your server. Add YAGPDB bot in your discord server from the top right tab next to your account name.
3. Make sure to give access to **ban** or **timeout** accounts based on your preferences. By default, this script timeout account for 24 hours.
4. Before edditing Command line, make sure discord server is selected.

#  Setting up Command line
1. In YAGPDB website, open **Custom Commands** in right tab. Press **Commands**.
2. In Commands, press **Create a new custom command**. This will open a new editor tab. Change the following settings:
3. Change **Trigger Type** to **Regex**.
4. Type ```[\s\S]+``` in **Trigger**.
5. Disable **Case Senstive?** and **Trigger on message edits too?** if enabled.
6. Enable **Command enabled?**.
7. Add this command in **Response**.
```
{{$msg := printf "⚠️ **Alert!** <@%d> sent a message in <#%d> and has been timed out!\n<@&ROLE_ID_1> <@&ROLE_ID_2>" .Member.User.ID .Channel.ID}}
{{sendMessage nil $msg}}

{{execAdmin "timeout" (str .Member.User.ID) "24h" "Sent message in add-channel-name"}}
```
You need to replace **ROLE_ID_1** and **ROLE_ID_2** with actual Discord role IDs. Here's how to get them:
Enable Developer Mode in Discord (Settings → Advanced → Developer Mode)
Right-click the role in Server Settings → Roles → Copy Role ID

Change **add-channel-name** to the channel you created in discord server.

8. If you want to add roles that are not effected by the bot, change **Role restrictions** to "ignore the roles in the following list", and add roles.
9. **Most importantly** change **Channel restrictions** to "Only run in the following channel" and add the channel you created.
10. Enable **Output errors as command response** and add channel that contains your server logs. It helps generate a proper error if something goes wrong.
11. Press **save**.

# Setting up Moderation
Now, we're going to enable bot moderation so that bot can timeout or ban the user.
1. Now go in **Moderation** → Moderation → Timeout.
2. Enable **Timeout**.
3. If you want to dm reason for the timeout or ban, add the message in **Timeout DM**.
4. Add the moderation and owner's role in **Users with the following roles will have permissoion to use the timeout related commands**.
5. Type 1440 in **Timeout duration in minutes**. 1440 min is equals to 24 hours.
6. Press **save**.

That's all you have to do to setup the bot. Now verify it by typing anything in that text channel and make sure that account does not have **mod** or **owner** role.
