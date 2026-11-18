# Demon_Cave

#Global varibles for the endings 
sleeping_powder = False
gnome = False
sword = False
#dictionary for the items and the and room discriptions didn't end up using the exits
game_map = { 
    "Garden": {
        "description": 
        """
        Lush wooded area that inside of a cave with streams and small lakes. 
        A door is at the end of the room there is a small lake between it and the player 
        above the lake is a fairy she wants a word.

        She tells you that she has a remdy for your problems a sleeping powder it can put anything to sleep
        for 1,000 years.



        """,
        "exits":"Demons hall",
       
        "Items":"Powerful sleeping powder"     
    },
   
    "The grave of the hero": {
      "description": """
        A small cold square room of stone, what lies in
        the middle is a sword of an anciant hero. The elder told you about it has the power to slay the
        beast. The exit is at the end of the room.
        """,
      
      "exits":"Demons hall",

      "Items":"Hero's sword"
    },
    
    "Gnome Hall": {
        "description": """
        A hallway that leads right to the lair of the beast.
        The only thing to meet you there is a Gnome the Gnome says that he has a solution
        to the beast and tells you a tale.

        Onece there was great Knight and his name was Logan. Logan had a family and a land he cared for deeply. 
        one day a nation invaded Logan's and he did not have the power to defend the things he cared for. Logan went to a witch, and 
        asked her to draw up a contract with a higher power so that he can defeat this nation on his own she did and Logan transformed. 
        He defeated the other nation with this great power but lost all the things that made him human. 
        
        Now he is the beast at the end of this cave if I was there I could have been there to help, but what I can do now is use this book.
        This book has an incantion that can turn him back to a human. Will you pick me up and help me cast the incation? 
        My names Garth nice to meet you. 


        """,
      
      "exits":"Demons hall",

      "Items":"Gnome"

      
    },

    "Domain of the beast": {
            "description": """


            You enter the the end of the cave, the domain of the beast. The beast's lair has rocky solid ground that is surrounded in lava.
            The beast lies at the end of the room it looks like a hairy hoofed creature with the head of horse, long horns
            and the torso of a man. The creature runs twords you and stops it looks at you as if it is investigating.


            """},

}
#Function for the sepreate endings based on what items you chose or don't choose
def endings(name):
    if sword:
        print(f"""
        
        All of your training has prepared you for this moment. {name} reacts and stabs the beast
        the beast didn't even have the chance to react. 
        The beast rolls on the floor in pain and begins it begings to steam and morph into
        what seems to be a man. The mystrious man has a hole in his chest bleeding and he lies dead. 
        {name} wonders who he was but not for long 
        and leaves the cave soon after. The village celebrates you as a hero and you live in peace. 

        THE END...

        """)

    if sleeping_powder:
        print(f"""
             
               You throw the sleeping powder in the face of the beast. The beast's claws stop short of {name}'s face. 
               The beast beast struggles to find its footing and eventualy collapses in a 1,000 year slumber it begins to dream.
               Perhaps due to the magical nature of the beast the dreams manifest as magical projections. The dream seems to be of 
               a man and his family. {name} wonders why a beast would dream of such things but not for long. {name} leaves the cave
               and back to the village. The village celebrates {name} as a hero and for the next 1,000 years the village lives in peace.

               THE END... 
    
                
                """)

    if gnome:
        print(f"""
            
            The Garth the Gnome tells you that he will hold off the beast while you read off the incantion. 
            Garth and the beast clash they seem equal. {name} reads the entire incantation and a flash of aura 
            from {name} transfers from them to the beast and the beast begings to clutch at his head and roar at the heavans. 
            While it morphs into the shape of a man. A long hair and bushy bearded man appaers from where the beast once stood
            they beging to weep. {name} relizes this is Logan {name} asks Logan if he would like to start a new life in the village.
            Logan accepts. Logan starts a new life in {name}'s village and live in peace and happiness.

            THE END. 
             
               """)

    if ((sword == False) and (sleeping_powder == False) and (gnome == False)):
        print(
            f"""
            You are unprepared and the monster ends you with one swipe of its claws.

            """
        )

def choose_sleep(name):
    choice = input("Use the powder or store it for later? ")
    if (choice == "store"):
        print("You put the powder in your bag and move on")
        print(f"{game_map['Domain of the beast']["description"]}")
        endings(name)
    elif(choice == "use"):
        print("""
        You use the powder and begin to dream. You know its the end for you, but at least you 
        will die in bliss of the dream and not have to worry about facing that scary monster.
        """)
    else: 
        print("You can't make up your mind if you want to USE or STORE the powder? (type use or store)")
        choose_sleep(name)
#Function that allows for the player choose and use items and will determine the ending you get
def choose_item(item, name, path):
    tmp = {
        "1": "Garden",
        "2": "The grave of the hero",
        "3": "Gnome Hall"
    }

    

    if (item == "yes"):
        print(f"You pick up {game_map[tmp[path]]["Items"]}")
        if (game_map[tmp[path]]["Items"] == "Powerful sleeping powder"):
                choose_sleep(name)
    elif (item == "no"):
        print(f"{name} moves on to the lair of the beast unprepared")
    elif (item=="fixme"):
        item = input("Pickup this item? ")
        choose_item(item, name, path)
    else:
        print("You stare into the wind like a deer in headlights...")
        choose_item("fixme", name, path)
#Function for choosing that path you take
def choose_path(name):
    path=input("What path will you chose? ")
    global sleeping_powder, sword, gnome

    match path:
        case "1":
            print(game_map["Garden"]["description"])

            item = input("Pickup this item? ")

            if(item=="yes"):
                sleeping_powder = True

            choose_item(item, name, path)
        case "2":
            print(game_map["The grave of the hero"]["description"])

            item = input("Pickup this item? ")

            if(item=="yes"):
                sword = True

            choose_item(item, name, path)
            endings(name)
            
        case "3":
            print(game_map["Gnome Hall"]["description"])

            item = input("Pickup this item? ")
            if(item=="yes"):
                gnome = True

            choose_item(item, name, path)
            endings(name)
        case _:
            print("You ran into a wall...Try again.")
            choose_path(name)
#main function and the begining of the game
def main():
    
    print("What is your hero's name?")
    name=input()
    print(f"""
    {name}, you must save our village and destroy the deamon in the great cave.
     When you enter the cave you must take the middle path or you will doom us all.
     """)

    print(f"""
    You take you journy outside of the village to the maw of the cave. {name} enters.
    The cave has 3 paths 1. Left 2. Middle 3. right. What will {name} choose?
    """)

    choose_path(name)

main()
