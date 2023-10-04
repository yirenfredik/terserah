# **HEROKU DEPLOY GUIDE**

---

## ***Heroku CLI Guide***

**Step 1 :** Git clone this Repo and change directory
> Make sure git is Installed in your system or quick run `apt-get install git pip curl -y`

```shell
git clone https://gitlab.com/mysterysd.sd/WZML-X && cd WZML-X 
```

**Step 2 :** Now Install Heroku in your Sytem or checkout Official Heroku Deploy Docs, or Download via `apt-get` or `npm`
> For Android : Use `termux` (Download via FDroid) for CLI usage

**The script requires sudo and isn’t Windows compatible.**
```shell
curl https://cli-assets.heroku.com/install.sh | sh
```

**Install with Ubuntu / Debian apt-get**
```shell
curl https://cli-assets.heroku.com/install-ubuntu.sh | sh
```

**Install via `npm` (Not Recommanded)**
```shell
npm install -g heroku
```

**Official Heroku Install Guide :** [Check Here](https://devcenter.heroku.com/articles/heroku-cli#install-the-heroku-cli)

**Step 3 :** Login into Heroku and Log In CLI via Browser 

_With Browser_
```shell
heroku login
```

**OR**

_Without Browser_
```shell
heroku login -i
```

- Put `Heroku Email` : Heroku Email `email@example.com`
- Put `Heroku Password` : Heroku API Key. Get from [Here](https://dashboard.heroku.com/account)

**Step 4 :** Create Heroku App and specify stack and region with App Name

```shell
heroku create --region us --stack container APP_NAME
```

**To Be Noted**: Copy the `BASE_URL` after the App is Created and Put the Value in `BASE_URL` when editing `config.env`

**Notes:**
- `--region eu` for Europe Server.
- `--region us` for United States Server.
- `APP_NAME` should be replaced with your unique app name _(Optional)_. If not given it generates a random name.
- `--stack container` for setting stack to container for Dockerfile.
- `--buildpack heroku/python` for using build slug for repo deploy and build.

**Step 5 :** Now set all the Required Variables and Files into this Branch MAIN Repo like config.env, accounts.zip, token.pickle, All Private Files(optional)- 
  > Only config.env Mabdatory with Only Mandatory Vars Only, After that Put all Private Files or Vars via Bot Settings `/bs`

**To Edit Inside CLI (nano Editor):** _(Termux Users)_
```shell
nano config.env
```
- **Sample config.env** _(Copy these and Paste in Editor and Fill Up)_
  ```
  BOT_TOKEN = ""
  TELEGRAM_API = ""
  TELEGRAM_HASH = ""
  OWNER_ID = ""
  UPSTREAM_REPO = ""
  UPSTREAM_BRANCH = "hk_wzmlx"
  DATABASE_URL = ""
  BASE_URL = ""
  TORRENT_TIMEOUT = "0"
  ```
- After Setup Exit from Editor via `CTRL + X`, followed via `y` and `Enter`...

**Helpful Commands:**
- **Exit from nano** : `CTRL + X`
- **Save File** : `CTRL + S`
- **Check Help** : `CTRL + G`
- **Undo Changes** : `ALT + U`
- ^ means CTRL _(Termux Users)_

**Step 6 :** Set Local git remote for Heroku. Give All Commands One by One.

```shell
git add . -f
git commit -m "HK Setup"
heroku git:remote -a APP_NAME
```

**Step 7 :** Now push to Heroku via git forcefully to build.

```shell
git push heroku main -f
```

**Heroku Logs:** When checking Logs, Use this will give Complete Logs.
```shell
heroku logs -a APP_NAME
```

- Add arg `-t` for Live Stream Logs and Use `CTRL + C` to Exit from it.

**All Heroku CLI Commands :** [Click Here](https://devcenter.heroku.com/articles/heroku-cli-commands#heroku-config-set)

---

## ***Variables Description:***

- `UPSTREAM_REPO`: GitLab repository URL, if your repo is private add `https://<deploy_token>:<password>@gitlab.com/<your_username>/<repository_name>
` format. `Str`.
  - **NOTE**: Don't forget to remove '<' and '>'. To generate gitlab Deploy Token. Follow [This](https://docs.gitlab.com/ee/user/project/deploy_tokens/#create-a-deploy-token)
              - Any change in docker you need to deploy/build again with updated repo to take effect. 
              - **No Need to delete .gitignore file or any File**
- `UPSTREAM_BRANCH`: Upstream branch for update. Default is `hk_wzmlx`. `Str`
- `BOT_TOKEN`: Telegram Bot Token that you got from [BotFather](https://t.me/BotFather). `Str`
- `OWNER_ID`: Telegram User ID (not username) of the Owner of the bot. `Int`
- `TELEGRAM_API`: This is to authenticate your Telegram account for downloading Telegram files. You can get this from <https://my.telegram.org>. `Int`
- `TELEGRAM_HASH`: This is to authenticate your Telegram account for downloading Telegram files. You can get this from <https://my.telegram.org>. `Str`
- `BASE_URL`: Valid BASE URL where the bot is deployed to use torrent web files selection. Format of URL should be `https://app-name-random_code.herokuapp.com/`, where `app-name` is the name of your heroku app Paste the URL got when the App was Made. `Str`
- `TORRENT_TIMEOUT`: Timeout of dead torrents downloading with qBittorrent and Aria2c in seconds. `Int`
  > Must Add else Bot Crashes! Set to 0 even not Needed
- `DATABASE_URL`: Database URL of MongoDb to store all your files and Vars. Adding this will be Helpful. `Str`

---

## ***Branch Specifications:***

- All files to be Uploaded in `main` Branch and set Upstream as `hk_wzmlx` Branch

---
