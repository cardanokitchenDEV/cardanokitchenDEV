import json
import random

from blockfrost import BlockFrostApi

#------------CONFIG-----------------------
api_key_mainnet = 'BLOCKFROSTTOKENID'
policy_id_ingredients = 'YOUR_POLICY_ID1'
policy_id_dishes = 'YOUR_POLICY_ID2'
out_file = 'FILENAME.txt'
#-----------------------------------------

api = BlockFrostApi(project_id=api_key_mainnet)

page = 1
assets_json = []
while True:
    response = api.assets_policy(policy_id=policy_id_ingredients, page=page)
    assets_json += response
    page += 1
    if len(response) == 0:
        break

print(f"{len(assets_json)} assets have been minted.")

all_addresses = list()
for asset in assets_json:
    addresses = api.asset_addresses(asset=asset.asset)
    all_addresses.append(addresses[0].address)

with open(out_file, 'w') as file:
    file.write(json.dumps(all_addresses))

statistics = dict()
for address in all_addresses:
    if address in statistics:
        statistics[address] = statistics[address] + 1
    else:
        statistics[address] = 1

winner = all_addresses[int(random.random()*len(all_addresses))]
print(f"And the winner is: {winner}")

sorted_by_count = sorted(list(statistics.items()), key=lambda x: x[1], reverse=True)
print(f"That's the stats: {sorted_by_count}")
