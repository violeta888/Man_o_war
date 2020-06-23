list_pirate_ship = list(map(lambda x: int(x), input().split('>')))
list_warship = list(map(lambda x: int(x), input().split('>')))
max_health_capacity = int(input())
line = input()


def fire():
    index = int(tokens[1])
    ship_sinks = False
    if (len(list_warship) - 1) >= index >= 0:
        damage = int(tokens[2])
        list_warship[index] -= damage
        if list_warship[index] <= 0:
            ship_sinks = True
        return ship_sinks



def defend():
    start_index = int(tokens[1])
    end_index = int(tokens[2])
    damage = int(tokens[3])
    pirate_ship_sinks = False
    if (len(list_pirate_ship) - 1) >= start_index >= 0 and (len(list_pirate_ship) - 1) >= end_index >= 0:
        for index_d in range(start_index, end_index + 1):
            list_pirate_ship[index_d] -= damage
            if list_pirate_ship[index_d] <= 0:
                pirate_ship_sinks = True
        return pirate_ship_sinks


def repair():
    index_r = int(tokens[1])
    health = int(tokens[2])
    if (len(list_warship) - 1) >= index_r >= 0:
        list_pirate_ship[index_r] += health
        if list_pirate_ship[index_r] > max_health_capacity:
            list_pirate_ship[index_r] = max_health_capacity
        return list_pirate_ship


def status():
    sections_need_repair = []
    min_health = max_health_capacity * 0.2
    for index_s in range(len(list_pirate_ship)):
        if list_pirate_ship[index_s] < min_health:
            sections_need_repair.append(list_pirate_ship[index_s])
    return len(sections_need_repair)


while True:
    tokens = line.split()
    command = tokens[0]
    if line == 'Retire':
        print(f'Pirate ship status: {sum(list_pirate_ship)}')
        print(f'Warship status: {sum(list_warship)}')
        break
    if command == 'Fire':
        fire()
        if fire():
            print('You won! The enemy ship has sunken.')
            break
    elif command == 'Defend':
        defend()
        if defend():
            print('You lost! The pirate ship has sunken.')
            break
    elif command == 'Repair':
        repair()
    elif command == 'Status':
        print(f'{status()} sections need repair.')

    line = input()
