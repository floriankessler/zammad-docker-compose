# How to use Zammad at msl.solutions

```bash
git clone git@github.com:floriankessler/zammad-docker-compose.git
#git remote add upstream git@github.com:zammad/zammad-docker-compose.git

git checkout master
docker compose -f docker-compose.yml -f docker-compose.override-msl.yml up -d
docker compose -f docker-compose.yml -f docker-compose.override-msl.yml logs -f
#docker compose -f docker-compose.yml -f docker-compose.override-msl.yml down
```

## Enter Zammad console

```bash
docker compose exec -it zammad-railsserver sh
docker compose exec -it zammad-railsserver rails c
```

## Upgrade Zammad

```bash
git checkout master
git pull upstream master
# Restart stack
```

## Set up Zammad

Mind you: "Groups" don't group agents but tickets! And allow for ACLs. And groups determine the mail address used for outgoing mails!
So you could group tickets into "Sales" or "Support" or "GF". Or, for now, group into "fke@gmx.de", to retain a more personal sender address.

http://support.msl.solutions

Manage
  Users | rename "Users" to "fke@gmx.de"
  Organizations | mindIP
  Trigger | disable "auto reply"
  Scheduler | "Delete spam"

Channels | Email
  Accounts | Email Accounts | fke@gmx.de
  Signatures | disable "default"
  Sender Format | set to "Agent Name"

Settings |
  System | Fully Qualified Domain Name
  Ticket | Base | Hook
  Ticket | Auto Assignment

## Flaws

UI just too unusable:

- No bulk merge
- No bulk operations on search results
- Clumsy bluk operations trigger (select, aim, drag, select, drop)

