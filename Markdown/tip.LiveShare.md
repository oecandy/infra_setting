# Tip. VSCode Live share

### 1. Install Live Share extention

1. Install the Visual Studio Live Share extension from the marketplace. 

2. Reload Visual Studio Code

3. Wait for dependencies to download and install (see status bar).

   

### 2. Sign in

In order to collaborate, you'll need to sign into Visual Studio Live Share so everyone knows who you are. This is purely a security measure and does not opt you into any marketing or other research activities. You can sign in using a Microsoft personal account (e.g. @outlook.com), Microsoft-backed work or school account (AAD), or a GitHub account. Signing in is easy.

Click on the `Live Share` status bar item or press `Ctrl+Shift+P` / `Cmd+Shift+P` and select the `Live Share: Sign In With Browser` command.



### 3. Using the Live Share viewlet

After installing Visual Studio Live Share, a custom tab will be added to the VS Code activity bar. In this tab, you can access all Live Share functions to collaborate. Additionally, when you share or join a collaboration session, a view will also appear in the Explorer tab for you to access all these functions as well.

![Live Share custom tab](./images/VSCdoe_Live_share/Vscode_coworker_list.png)

![Live Share explorer view](./images/VSCdoe_Live_share/vscode-explorer-view.png)

With these views, you can see a participant's location in the shared code, click on a participant to follow them, focus participants, access shared servers and terminals, and more.



### 4. Share a project

After downloading and installing Visual Studio Live Share, follow these steps to start a collaboration session and invite a colleague to work with you.

1. **Sign in**

   After installing the Live Share extension, reloading, and waiting for dependencies to finish installing, you'll want to sign in to let other collaborators know who you are. See [sign in](https://docs.microsoft.com/en-us/visualstudio/liveshare/use/vscode#sign-in) for more details.

2. **Open a folder**

   Use your normal workflow to open a folder, project, or solution you would like to share with your guests.

3. **[Optional] Update hidden or excluded files**

   By default, Live Share **hides** any files/folders referenced in .gitignore files in your shared folders from guests. **Hiding** a file prevents it from appearing in the guest's file tree. **Excluding** a file applies a stricter rule that will prevent Live Share from opening it for the guest in situations like go to a definition or if you step into the file while debugging or being "followed". If you want to hide/exclude different files, a **.vsls.json** file can be added to your project with these settings. See [controlling file access and visibility](https://docs.microsoft.com/en-us/visualstudio/liveshare/reference/security#controlling-file-access-and-visibility) for details.

4. **Start a collaboration session**

   Now, simply **click** the "Live Share" status bar item or hit **Ctrl+Shift+P / Cmd+Shift+P** and select "Live Share: Start a collaboration session (Share)".

   ![Share button](./images/VSCdoe_Live_share/vscode-share-button-new.png)

   * ***Note**

   ```
   You may be asked by your desktop firewall software to allow the Live Share agent to open a port the first time you share. Accepting this is entirely optional but enables a secured "direct mode" to improve performance when the person you are working with is on the same network as you are. See [changing the connection mode](https://docs.microsoft.com/en-us/visualstudio/liveshare/reference/connectivity#changing-the-connection-mode) for details.
   ```

   An invite link will be automatically copied to your clipboard. When opened in a browser, this link allows others to join a new collaboration session that shares contents of these folders with them.

   You will also see the "Live Share" status bar item transition to represent the session state. See [session state](https://docs.microsoft.com/en-us/visualstudio/liveshare/use/vscode#session-states) information below for what this looks like.

   Note that if you need to get the invite link again after you've started sharing, you access it again by clicking on the session state status bar icon and select "Invite Others (Copy Link)".

5. **[Optional] Enable read-only mode**

   Once you start your collaboration session, you can set the session to be read-only to prevent guests from making edits to the code being shared.

   After sharing, you will get a notification that the invite link has been copied to your clipboard. You can then select the option to make the session read-only.

   ![VS Code Read-only mode](./images/VSCdoe_Live_share/vscode-read-only-toast.png)

6. **Send someone the link**

   Send the link over e-mail, Slack, Skype, etc. to those you want to invite. Note that, given the level of access Live Share sessions can provide to guests, **you should only share with people you trust** and think through the implications of what you are sharing.

   > **Security Tip:** Want to understand the security implications of some of Live Share's features? Check out the [security](https://docs.microsoft.com/en-us/visualstudio/liveshare/reference/security) article.

   If the guest you invited has questions, the "[Quickstart: Join your first session](https://docs.microsoft.com/en-us/visualstudio/liveshare/quickstart/join)" article provides some more information on getting up and running as a guest.

7. **[Optional] Approve the guest**

   By default, guests will automatically join your collaboration session and you'll be notified when they're ready to work with you. While this notification gives you the option to remove them from the session, you can also opt to instead require an explicit "approval" for anyone joining.

   To enable this feature, simply add the following to settings.json:

   ```json
   "liveshare.guestApprovalRequired": true
   ```

   Once you have this setting turned on, a notification will prompt you to approve the guest before they can join.

   ![Visual Studio Code join approval request](./images/VSCdoe_Live_share/vscode-join-approval.png)

   See [invitations and join access](https://docs.microsoft.com/en-us/visualstudio/liveshare/reference/security#invitations-and-join-access) for additional details on invitation security considerations.



### 5. Stop the collaboration session

As a host, you can stop sharing completely and end the collaboration session at any time by opening the Live Share view in the Explorer or in the Live Share custom tab and selecting the "Stop collaboration session" icon.

![Stop collaboration session](./images/VSCdoe_Live_share/vscode-end-collaboration-viewlet.png)

All guests will be notified that the session has ended. Once the session has ended, guests will no longer be able to access the content and any temp files are automatically cleaned up.

Having issues with sharing? Check out [troubleshooting](https://docs.microsoft.com/en-us/visualstudio/liveshare/troubleshooting#share-and-join).

### 6. Join a collaboration session

After downloading and installing Visual Studio Live Share, guests only need to take a couple of steps to join a hosted collaboration session. There are two ways to join: [via the browser](https://docs.microsoft.com/en-us/visualstudio/liveshare/use/vscode#join-via-the-browser) and [manually](https://docs.microsoft.com/en-us/visualstudio/liveshare/use/vscode#join-manually).

> **Security Tip:** As a guest joining a collaboration session, it's important to understand that hosts may restrict your access to certain files or features. Want to understand the security implications of some of Live Share's features and settings? Check out the [security](https://docs.microsoft.com/en-us/visualstudio/liveshare/reference/security) article.

#### Join via the browser

The easiest way to join a collaboration session is to simply open the invite link in a web browser. Here's what you can expect when you follow this flow.

1. **Sign in**

   After installing the Live Share extension, reloading, and waiting for dependencies to finish installing, you'll want to sign in to let other collaborators know who you are. See [sign in](https://docs.microsoft.com/en-us/visualstudio/liveshare/use/vscode#sign-in) for more details.

2. **Click on the invite link / open the invite in your browser**

   Now, simply open (or re-open) the invite link in a browser.

   > **Note**: If you have not yet installed the Live Share extension, you'll be presented with links to the extension marketplace. Install the extension and restart your tool and retry.

   You should be notified that the browser wants to launch a Live Share enabled tool. If you let it launch your selected tool, you'll be connected to the collaboration session once it starts.

   ![Join page](./images/VSCdoe_Live_share/join-page.png)

   If the host is offline, you'll be notified at this point instead. You can then contact the host and ask them to share again.

   *  **Note**

     Be sure you've **started the tool at least once** after installing the Visual Studio Live Share extension and allowed the installation to finish before opening/re-opening the invite page. Still having trouble? See [join manually](https://docs.microsoft.com/en-us/visualstudio/liveshare/use/vscode#join-manually).

3. **Collaborate**

   That's it! In a few moments you'll be connected and you can start collaborating.

   You will see the "Live Share" button transition to convey a "Session State". See [session state](https://docs.microsoft.com/en-us/visualstudio/liveshare/use/vscode#session-states) information below for what this looks like.

   You'll then be automatically taken to the file the host is currently editing once the join is complete.



### 7. Join manually

You can also manually join without using a web browser which can be useful in situations where the tool you want to use is already running, you want to use a different tool than you usually do, or if you are having trouble with getting invite links to work for some reason. The process is easy:

1. **Sign in**

   After installing the Live Share extension, reloading, and waiting for dependencies to finish installing, you'll want to sign in to let other collaborators know who you are. See [sign in](https://docs.microsoft.com/en-us/visualstudio/liveshare/use/vscode#sign-in) for more details.

2. **Use the join command**

   Open the Live Share custom tab in the VS Code activity bar, and select the "Join collaboration session..." icon or entry.

   ![Join viewlet icon](./images/VSCdoe_Live_share/vscode-join-viewlet.png)

3. **Paste the invite link**

   Paste in the invite URL you were sent and hit enter to confirm.

4. **Collaborate!**

   That's it! You should be connected to the collaboration session momentarily.

   You will see the "Live Share" button transition to convey a "Session State". See [session state](https://docs.microsoft.com/en-us/visualstudio/liveshare/use/vscode#session-states) information below for what this looks like.

   You'll then be automatically taken to the file the host is currently editing once the join is complete.

### 8. Leave the collaboration session

As a guest, you can leave the collaboration session without ending it for others by simply closing the VS Code window. If you'd prefer to keep the window open, you can open the Live Share Explorer view or the Live Share custom tab and select the "Leave collaboration session" icon.

![Leaves session icon](./images/VSCdoe_Live_share/vscode-leave-session-viewlet.png)

Any temp files are automatically cleaned up so no further action is needed.



### 9. Co-editing

Once a guest has joined a collaboration session, all collaborators will immediately be able to see each other's edits and selections in real-time. All you need to do is pick a file from the file explorer and start editing. Both hosts and guests will see edits as you make them and can contribute themselves making it easy iterate and rapidly nail to down solutions.

* **Note**

  Joining a read-only collaboration session prevents guests from being able to make edits to files. A host can [enable read-only mode when they share](https://docs.microsoft.com/en-us/visualstudio/liveshare/use/vscode#share-a-project). As a guest, you can tell if you have joined a read-only session by looking at your [session state](https://docs.microsoft.com/en-us/visualstudio/liveshare/use/vscode#session-states).

![Screen shot showing co-editing](./images/VSCdoe_Live_share/vscode-coedit.png)

* **Note**

  Co-editing has limitations for certain languages. See [platform support](https://docs.microsoft.com/en-us/visualstudio/liveshare/reference/platform-support) for the state of features by language.

Beyond cursors and edits, selections you make are also visible to all participants in that same file. This makes it easy to highlight where problems might exist or convey ideas.

![Screen shot showing highlighting](./images/VSCdoe_Live_share/vscode-highlight.png)

Better yet, you and other participants can navigate to any file in the shared project. You can either edit together or independently meaning you can seamlessly switch between investigation, making small tweaks and full collaborative editing.

The resulting edits are persisted on the host's machine on save so there is no need to synchronize, push, or send files around once you're done editing. The edits are "just there."