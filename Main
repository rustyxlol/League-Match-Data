import requests
import json
import csv
import time
headerList = ['gameId', 'gameDuration', 'team', 'champion', 'wins', 'kills', 'deaths', 'assists',
              'longestTimeSpentLiving', 'largestKillingSpree', 'largestMultiKill', 'killingSprees', 'doubleKills',
              'tripleKills', 'quadraKills', 'pentaKills', 'unrealKills', 'totalDamageDealt', 'magicDamageDealt',
              'physicalDamageDealt', 'trueDamageDealt', 'largestCriticalStrike', 'totalDamageDealtToChampions',
              'magicDamageDealtToChampions', 'physicalDamageDealtToChampions', 'trueDamageDealtToChampions',
              'totalHeal', 'damageDealtToTurrets', 'timeCCingOthers', 'totalDamageTaken', 'magicalDamageTaken',
              'physicalDamageTaken', 'trueDamageTaken', 'goldEarned', 'goldSpent', 'totalMinionsKilled', 'turretKills',
              'inhibitorKills']


def get_player(cId, match_data):
    for i in range(10):
        if str(cId) == str(match_data['participants'][i]['championId']):
            return int(i)


def get_match_details(gameId):
    mURL = "https://euw1.api.riotgames.com/lol/match/v4/matches/" + str(
        gameId) + "?api_key="+API
    mResponse = requests.get(mURL)
    match_data = mResponse.json()
    return match_data


def get_stats(match_data, participant, championName, csv_writer):
    gameId = match_data['gameId']
    gameDuration = match_data['gameDuration']
    team = match_data['participants'][participant]['teamId']
    if team is 100:
        team = "blue"
    else:
        team = "red"
    wins = match_data['participants'][participant]['stats']['win']
    kills = match_data['participants'][participant]['stats']['kills']
    deaths = match_data['participants'][participant]['stats']['deaths']
    assists = match_data['participants'][participant]['stats']['assists']
    longestTimeSpentLiving = match_data['participants'][participant]['stats']['longestTimeSpentLiving']
    largestKillingSpree = match_data['participants'][participant]['stats']['largestKillingSpree']
    largestMultiKill = match_data['participants'][participant]['stats']['largestMultiKill']
    killingSprees = match_data['participants'][participant]['stats']['killingSprees']
    doubleKills = match_data['participants'][participant]['stats']['doubleKills']
    tripleKills = match_data['participants'][participant]['stats']['tripleKills']
    quadraKills = match_data['participants'][participant]['stats']['quadraKills']
    pentaKills = match_data['participants'][participant]['stats']['pentaKills']
    unrealKills = match_data['participants'][participant]['stats']['unrealKills']
    totalDamageDealt = match_data['participants'][participant]['stats']['totalDamageDealt']
    magicDamageDealt = match_data['participants'][participant]['stats']['magicDamageDealt']
    physicalDamageDealt = match_data['participants'][participant]['stats']['physicalDamageDealt']
    trueDamageDealt = match_data['participants'][participant]['stats']['trueDamageDealt']
    largestCriticalStrike = match_data['participants'][participant]['stats']['largestCriticalStrike']
    totalDamageDealtToChampions = match_data['participants'][participant]['stats']['totalDamageDealtToChampions']
    magicDamageDealtToChampions = match_data['participants'][participant]['stats']['magicDamageDealtToChampions']
    physicalDamageDealtToChampions = match_data['participants'][participant]['stats']['physicalDamageDealtToChampions']
    trueDamageDealtToChampions = match_data['participants'][participant]['stats']['trueDamageDealtToChampions']
    totalHeal = match_data['participants'][participant]['stats']['totalHeal']
    damageDealtToTurrets = match_data['participants'][participant]['stats']['damageDealtToTurrets']
    timeCCingOthers = match_data['participants'][participant]['stats']['timeCCingOthers']
    totalDamageTaken = match_data['participants'][participant]['stats']['totalDamageTaken']
    magicalDamageTaken = match_data['participants'][participant]['stats']['magicalDamageTaken']
    physicalDamageTaken = match_data['participants'][participant]['stats']['physicalDamageTaken']
    trueDamageTaken = match_data['participants'][participant]['stats']['trueDamageTaken']
    goldEarned = match_data['participants'][participant]['stats']['goldEarned']
    goldSpent = match_data['participants'][participant]['stats']['goldSpent']
    totalMinionsKilled = match_data['participants'][participant]['stats']['totalMinionsKilled']
    turretKills = match_data['participants'][participant]['stats']['turretKills']
    inhibitorKills = match_data['participants'][participant]['stats']['inhibitorKills']
    csv_writer.writerow(
        [gameId, gameDuration, team, championName, wins, kills, deaths, assists, longestTimeSpentLiving,
         largestKillingSpree,
         largestMultiKill, killingSprees, doubleKills, tripleKills, quadraKills, pentaKills, unrealKills,
         totalDamageDealt, magicDamageDealt, physicalDamageDealt, trueDamageDealt, largestCriticalStrike,
         totalDamageDealtToChampions, magicDamageDealtToChampions, physicalDamageDealtToChampions,
         trueDamageDealtToChampions, totalHeal, damageDealtToTurrets, timeCCingOthers, totalDamageTaken,
         magicalDamageTaken, physicalDamageTaken, trueDamageTaken, goldEarned, goldSpent, totalMinionsKilled,
         turretKills, inhibitorKills])
    print("Game ID: ", match_data['gameId'], "DONE")


def init():
    requests.get(
        "https://euw1.api.riotgames.com/lol/summoner/v4/summoners/by-name/Rusty+WD?api_key="+API)

    aid = requests.get('https://euw1.api.riotgames.com/lol/summoner/v4/summoners/by-name/Rusty+WD?api_key='+API)
    r = aid.json()
    accountId= r['accountId']

    mlist = requests.get('https://euw1.api.riotgames.com/lol/match/v4/matchlists/by-account/'+accountId+'?queue=450&api_key='+API)
    match_list_file = mlist.json()

    csv_file = open('C:/Users/drdem/Desktop/Desktop/Programming/PyLibraries/Leauge shit/matchWHOLE.csv', 'a+',
                    newline='')
    csv_writer = csv.writer(csv_file)
    csv_writer.writerow(headerList)
    matches = match_list_file['matches']
    champion_dict = requests.get("https://ddragon.leagueoflegends.com/cdn/11.6.1/data/en_US/champion.json").json()
    id_to_name = {data["key"]: data["name"] for _, data in champion_dict["data"].items()}

    for index, i in enumerate(matches):
        match_data = get_match_details(i['gameId'])
        participant = int(get_player(i['champion'], match_data))
        champion = str(i['champion'])
        championName = id_to_name[champion]
        print(championName)
        get_stats(match_data, participant, championName, csv_writer)
        print("Index: ", index, " Done")
        if index % 50 is 0:
            time.sleep(30)


def main():
    init()

if __name__ == "__main__":
    main()
