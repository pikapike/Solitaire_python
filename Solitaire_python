# Solitaire - a card game 
# Stack cards such as to put in a sequence of ranks
# like directly lower values on top of a value ex. 8 on 9, A on 2
# goal is to eliminate progressions of KQJT98765432A
# Deal if you are stuck
# New game if you are screwed

import simplegui
import random

# load card sprite - 949x392 - source: jfitz.com
CARD_SIZE = (73, 98)
CARD_CENTER = (36.5, 49)
card_images = simplegui.load_image("http://commondatastorage.googleapis.com/codeskulptor-assets/cards.jfitz.png")

CARD_BACK_SIZE = (71, 96)
CARD_BACK_CENTER = (35.5, 48)
card_back = simplegui.load_image("http://commondatastorage.googleapis.com/codeskulptor-assets/card_back.png")    

CARD_SPACE = 75
MARGIN = 35

# initialize some useful global variables
score = 0
turns = 0
actual_turns = turns / 1
deals_left = 6
game_mode = "easy"

# define globals for cards
SUITS = ('C', 'S', 'H', 'D')
RANKS = ('A', '2', '3', '4', '5', '6', '7', '8', '9', 'T', 'J', 'Q', 'K')
VALUES = {'A':1, '2':2, '3':3, '4':4, '5':5, '6':6, '7':7, '8':8, '9':9, 'T':10, 'J':11, 'Q':12, 'K':13}
DUPES = ("R", "D")
COLOR = {'C':1, 'S':1, 'H':0, 'D':0}
# define card class
class Card:
    def __init__(self, suit, rank, dupe):
        self.up = False
        if (suit in SUITS) and (rank in RANKS) and (dupe in DUPES):
            self.suit = suit
            self.rank = rank
            self.dupe = dupe
        else:
            self.suit = None
            self.rank = None
            self.dupe = None
            print "Invalid card: ", suit, rank

    def __str__(self):
        return self.suit + self.rank

    def get_suit(self):
        return self.suit

    def get_rank(self):
        return self.rank
    
    def flip(self):
        if self.up == True:
            self.up = False
        else:
            self.up = True

    def draw(self, canvas, pos):
        if self.up == True:
            card_loc = (CARD_CENTER[0] + CARD_SIZE[0] * (VALUES.get(self.rank)-1),
                        CARD_CENTER[1] + CARD_SIZE[1] * SUITS.index(self.suit))
            canvas.draw_image(card_images, card_loc, CARD_SIZE,
                              [pos[0] + CARD_CENTER[0], pos[1] + CARD_CENTER[1]], CARD_SIZE)
        else:
            card_loc = CARD_BACK_CENTER
            canvas.draw_image(card_back, card_loc, CARD_BACK_SIZE, 
                              [pos[0] + CARD_BACK_CENTER[0], pos[1] + CARD_BACK_CENTER[1]], CARD_BACK_SIZE)
        
# define hand class
class Hand:
    def __init__(self):
        self.hand = []

    def __str__(self):
        string = "Hand contains"
        for card in self.hand:
            string += " " + str(card)
        return string
    
    def card_up_count(self):
        n = 0
        for card in self.hand:
            if card.up == True:
                n += 1
        return n
    
    def add_card(self, card):
        self.hand.append(card)

    def get_value(self):
        sum = 0
        check = 0
        for card in self.hand:
            sum += VALUES.get(card.get_rank())
            if card.get_rank() == "A":
                check = 1
        if check == 1:
            if sum < 12:
                return sum + 10
            else:
                return sum
        else:
            return sum
   
    def deal_card(self):
        a = random.choice(self.hand)
        self.hand.remove(a)
        return a
    
    def give_card(self, position):
        a = self.hand[position]
        self.hand.remove(a)
        return a
    
    def show_rank(self, position):
        a = self.hand[position]
        return a.get_rank()
    
    def unhide(self):
        try:
            if self.hand[-1].up == False:
                self.hand[-1].flip()
        except:
            pass
        
    def draw(self, canvas, pos):
        i = 0
        while i < len(self.hand):
            self.hand[i].draw(canvas, [pos[0], pos[1]+20*i])
            i += 1

            
    def clear(self):
        i = 0
        j = len(self.hand)
        while i < j:
            try:
                self.hand.pop(0)
            except:
                pass
            i += 1
        
# define deck class 
class Deck:
    def __init__(self):
        self.cards = []
        for suit in SUITS:
            for rank in RANKS:
                for dupe in DUPES:
                    card = Card(suit, rank, dupe)
                    self.cards.append(card)

    def shuffle(self):
        random.shuffle(self.cards)

    def deal_card(self):
        """if self.cards == []:
            for suit in SUITS:
                for rank in RANKS:
                    card = Card(suit, rank)
                    self.cards.append(card)"""
        a = random.choice(self.cards)
        self.cards.remove(a)
        return a

    
    def __str__(self):
        string = "Deck contains"
        for card in self.cards:
            string += " " + str(card)
        return string

passout_deck = Deck()
hand1 = Hand()
hand2 = Hand()
hand3 = Hand()
hand4 = Hand()
hand5 = Hand()
hand6 = Hand()
hand7 = Hand()
hand8 = Hand()
deck1 = Hand()
deck2 = Hand()
deck3 = Hand()
deck4 = Hand()
deck5 = Hand()
deck6 = Hand()
choice1 = None
choice2 = None

def new_game():
    global hand1, hand2, hand3, hand4, hand5, hand6, hand7, hand8, score, deals_left
    global deck1, deck2, deck3, deck4, deck5, deck6, passout_deck, turns
    score = 0
    turns = 0
    deals_left = 6
    hand1 = Hand()
    hand2 = Hand()
    hand3 = Hand()
    hand4 = Hand()
    hand5 = Hand()
    hand6 = Hand()
    hand7 = Hand()
    hand8 = Hand()
    deck1 = Hand()
    deck2 = Hand()
    deck3 = Hand()
    deck4 = Hand()
    deck5 = Hand()
    deck6 = Hand()
    passout_deck = Deck()
    i = 0
    while i < 7:
        hand1.add_card(passout_deck.deal_card())
        i += 1
    hand1.unhide()
    i = 0
    while i < 7:
        hand2.add_card(passout_deck.deal_card())
        i += 1
    hand2.unhide()
    i = 0
    while i < 7:
        hand3.add_card(passout_deck.deal_card())
        i += 1
    hand3.unhide()
    i = 0
    while i < 7:
        hand4.add_card(passout_deck.deal_card())
        i += 1
    hand4.unhide()
    i = 0
    while i < 7:
        hand5.add_card(passout_deck.deal_card())
        i += 1
    hand5.unhide()
    i = 0
    while i < 7:
        hand6.add_card(passout_deck.deal_card())
        i += 1
    hand6.unhide()
    i = 0
    while i < 7:
        hand7.add_card(passout_deck.deal_card())
        i += 1
    hand7.unhide()
    i = 0
    while i < 7:
        hand8.add_card(passout_deck.deal_card())
        i += 1
    hand8.unhide()
    i = 0
    while i < 8:
        deck1.add_card(passout_deck.deal_card())
        i += 1
    i = 0
    while i < 8:
        deck2.add_card(passout_deck.deal_card())
        i += 1
    i = 0
    while i < 8:
        deck3.add_card(passout_deck.deal_card())
        i += 1
    i = 0
    while i < 8:
        deck4.add_card(passout_deck.deal_card())
        i += 1
    i = 0
    while i < 8:
        deck5.add_card(passout_deck.deal_card())
        i += 1
    i = 0
    while i < 8:
        deck6.add_card(passout_deck.deal_card())
        i += 1
    
    """for hand in set_of_hands:
        i = 0
        while i < 7:
            b = passout_deck.deal_card()
            hand.add_card(b)
            print hand
            i += 1
    for deck in set_of_decks:
        i = 0
        while i < 8:
            deck.add_card(passout_deck.deal_card())
            i += 1"""

def value(card):
    return VALUES.get(card.rank)
    
def deal():
    global deck1, deck2, deck3, deck4, deck5, deck6, turns, actual_turns, hand1, deals_left
    turns += 1
    deals_left -= 1
    actual_turns = int(turns - (turns % 1))
    if len(deck1.hand) == 0:
        if len(deck2.hand) == 0:
            if len(deck3.hand) == 0:
                if len(deck4.hand) == 0:
                    if len(deck5.hand) == 0:
                        if len(deck6.hand) == 0:
                            turns -= 1
                            actual_turns = int(turns - (turns % 1))
                            deals_left += 1
                        else:
                            hand1.add_card(deck6.deal_card())
                            hand2.add_card(deck6.deal_card())
                            hand3.add_card(deck6.deal_card())
                            hand4.add_card(deck6.deal_card())
                            hand5.add_card(deck6.deal_card())
                            hand6.add_card(deck6.deal_card())
                            hand7.add_card(deck6.deal_card())
                            hand8.add_card(deck6.deal_card())
                    else:
                        hand1.add_card(deck5.deal_card())
                        hand2.add_card(deck5.deal_card())
                        hand3.add_card(deck5.deal_card())
                        hand4.add_card(deck5.deal_card())
                        hand5.add_card(deck5.deal_card())
                        hand6.add_card(deck5.deal_card())
                        hand7.add_card(deck5.deal_card())
                        hand8.add_card(deck5.deal_card())
                else:
                    hand1.add_card(deck4.deal_card())
                    hand2.add_card(deck4.deal_card())
                    hand3.add_card(deck4.deal_card())
                    hand4.add_card(deck4.deal_card())
                    hand5.add_card(deck4.deal_card())
                    hand6.add_card(deck4.deal_card())
                    hand7.add_card(deck4.deal_card())
                    hand8.add_card(deck4.deal_card())
            else:
                hand1.add_card(deck3.deal_card())
                hand2.add_card(deck3.deal_card())
                hand3.add_card(deck3.deal_card())
                hand4.add_card(deck3.deal_card())
                hand5.add_card(deck3.deal_card())
                hand6.add_card(deck3.deal_card())
                hand7.add_card(deck3.deal_card())
                hand8.add_card(deck3.deal_card())
        else:
            hand1.add_card(deck2.deal_card())
            hand2.add_card(deck2.deal_card())
            hand3.add_card(deck2.deal_card())
            hand4.add_card(deck2.deal_card())
            hand5.add_card(deck2.deal_card())
            hand6.add_card(deck2.deal_card())
            hand7.add_card(deck2.deal_card())
            hand8.add_card(deck2.deal_card())
    else:
        hand1.add_card(deck1.deal_card())
        hand2.add_card(deck1.deal_card())
        hand3.add_card(deck1.deal_card())
        hand4.add_card(deck1.deal_card())
        hand5.add_card(deck1.deal_card())
        hand6.add_card(deck1.deal_card())
        hand7.add_card(deck1.deal_card())
        hand8.add_card(deck1.deal_card())
    hand1.unhide()
    hand2.unhide()
    hand3.unhide()
    hand4.unhide()
    hand5.unhide()
    hand6.unhide()
    hand7.unhide()
    hand8.unhide()
    
def mouseclick(position):
    global hand1, hand2, hand3, hand4, hand5, hand6, hand7, hand8
    global score, turns, actual_turns, choice1, choice2, game_mode
    set_of_hands = [hand1, hand2, hand3, hand4,
                    hand5, hand6, hand7, hand8]
    hand_position = None
    if (position[0] > MARGIN) and (position[0] < 9*CARD_SPACE - MARGIN):
        turns += 0.5
        hand_position = ((position[0] - MARGIN - 10) / CARD_SPACE)
        if turns % 1 == 0.5:
            choice1 = hand_position
            chosen_hand1 = set_of_hands[choice1]
            if chosen_hand1.card_up_count() > 12:
                rank_list = []
                i = 0
                for i in range(0, 13):
                    i += 1
                    rank_list.append(chosen_hand1.show_rank(-i))
                if rank_list == ['A', '2', '3', '4', '5', '6', '7', '8', '9', 'T', 'J', 'Q', 'K']:
                    score += 1
                    if game_mode == "hard":
                        score += 2
                    i = 0
                    while i < 13:
                        chosen_hand1.hand.pop()
                        i += 1
                    chosen_hand1.unhide()
                    turns -= 0.5
        if turns % 1 == 0:
            choice2 = hand_position
            chosen_hand2 = set_of_hands[choice2]
            chosen_hand1 = set_of_hands[choice1]
            if len(chosen_hand2.hand) == 0:
                i = 1
                while i <= chosen_hand1.card_up_count():
                    chosen_hand2.add_card(chosen_hand1.give_card(-i))
                chosen_hand1.unhide()
            else:
                front_card = value(set_of_hands[choice2].hand[-1])
                if choice1 == choice2:
                    turns -= 1
                elif len(chosen_hand1.hand) == 0:
                    turns -= 1
                elif len(chosen_hand2.hand) == 0:
                    i = 0
                    n = chosen_hand1.card_up_count()
                    break_it = 0
                    while i < n:
                        try:
                            if value(chosen_hand1.hand[i-n]) != value(chosen_hand1.hand[-i-n+1]) - 1:
                                break_it = 1
                        except:
                            pass
                        if break_it == 1:
                            continue
                        chosen_hand2.add_card(chosen_hand1.give_card(i-n))
                else:
                    i = 1
                    good = 0
                    break_it = 0
                    while i <= chosen_hand1.card_up_count():
                        if value(chosen_hand1.hand[-i]) == front_card - 1:
                            good = 1
                            break_it = 1
                        try:
                            if value(chosen_hand1.hand[-i]) != value(chosen_hand1.hand[-i-1]) - 1:
                                break_it = 1
                        except:
                            pass
                        if break_it == 1:
                            break
                        i += 1
                    if good == 1:
                        if (COLOR.get(chosen_hand1.hand[-i].get_suit()) == COLOR.get(chosen_hand2.hand[-1].get_suit())) and (game_mode == "hard"):
                            turns -= 1
                        else:
                            j = 0
                            while j < i:
                                chosen_hand2.add_card(chosen_hand1.give_card(-i+j))
                                j += 1
                            chosen_hand1.unhide()
                    else:
                        turns -= 1
    elif turns % 1 == 0.5:
        turns -= 0.5
    actual_turns = int(turns - (turns % 1))
    
def switch_modes():
    global game_mode
    new_game()
    if game_mode == "easy":
        game_mode = "hard"
    else:
        game_mode = "easy"
    
# draw handler    
def draw(canvas):
    global actual_turns, score, game_mode
    display_turns = "Turns: " + str(actual_turns)
    hand1.draw(canvas, [CARD_SPACE / 2, 50])
    hand2.draw(canvas, [3*CARD_SPACE / 2, 50])
    hand3.draw(canvas, [5*CARD_SPACE / 2, 50])
    hand4.draw(canvas, [7*CARD_SPACE / 2, 50])
    hand5.draw(canvas, [9*CARD_SPACE / 2, 50])
    hand6.draw(canvas, [11*CARD_SPACE / 2, 50])
    hand7.draw(canvas, [13*CARD_SPACE / 2, 50])
    hand8.draw(canvas, [15*CARD_SPACE / 2, 50])
    canvas.draw_text(display_turns, [50, 40], 40, "White")
    canvas.draw_text("Score: "+ str(score), [250, 40], 40, "White")
    canvas.draw_text("Deals left:" + str(deals_left),
                     [400, 40], 40, "White")
    canvas.draw_text(game_mode, [10, 580], 20, "White")

# initialization frame
frame = simplegui.create_frame("Solitaire", 9*CARD_SPACE, 600)
frame.set_canvas_background("Green")

#create buttons and canvas callback
frame.set_draw_handler(draw)
frame.add_button("New game", new_game)
frame.set_mouseclick_handler(mouseclick)
frame.add_button("Deal", deal)
frame.add_label("Deal if you are stuck")
frame.add_label("      ")
frame.add_label("Stack the cards so that")
frame.add_label("they stack from highest")
frame.add_label("tier to lowest tier")
frame.add_label("        ")
frame.add_label("Eliminate stacks of: ")
frame.add_label('KQJT98765432A')
frame.add_label("by clicking on them")
frame.add_label("     ")
frame.add_label("Move cards by clicking")
frame.add_label("the thing you want to move")
frame.add_label("then the thing to move it on")
frame.add_button("Switch levels", switch_modes)
                

# get things rolling
frame.start()
new_game()


# remember to review the gradic rubric
