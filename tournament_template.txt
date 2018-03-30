
# Author: Mark Catugas 

#----------------- Preliminary Round Setup -------------------

def pbtournamentPrelimSetup  
  tr1 = [PBTrainers::YOUNGSTER,"Isidore",_I("Eff you gayboy."),false,0,true,0]
  tr2 = [PBTrainers::PRYCE,"Pryce",_I("Ah, I am impressed by your prowess."),false,0,true,0]
  tr3 = [PBTrainers::CANDICE,"Candice",_I("I must say, I've warmed up to you!"),false,0,true,0]
  tr4 = [PBTrainers::LEADER_Misty,"Misty",_I("I can't believe I lost!"),false,0,true,0]
  tr5 = [PBTrainers::ENGINEER,"Mark (Village Cup Champ)",_I("Hmmm, it seems I've made a miscalculation."),false,0,true,0]
  tr6 = [PBTrainers::SAILOR,"Oca (Wilds Cup Finalist)",_I("Dangit, I'm so tilted now!"),false,0,true,0]
  tr7 = [PBTrainers::HIKER,"Josh (Northshore Finalist)",_I("Nooo, how did everything go so wrong?!"),false,0,true,0]

  $boardplace = []
  battleplace = []
  
  $prelimRound = true
  $semiRound = false
  $finalRound = false

  t1picked = false
  t2picked = false
  t3picked = false
  t4picked = false
  t5picked = false   
  t6picked = false   
  t7picked = false   
    
  begin
    randplace = rand(7)
    if randplace == 0 && t1picked == false
        $boardplace.unshift(tr1[1])
        battleplace.unshift(tr1)
        t1picked = true
    elsif randplace == 1 && t2picked == false
        $boardplace.unshift(tr2[1])
        battleplace.unshift(tr2)
        t2picked = true
    elsif randplace == 2 && t3picked == false
        $boardplace.unshift(tr3[1])
        battleplace.unshift(tr3)
        t3picked = true
    elsif randplace == 3 && t4picked == false
        $boardplace.unshift(tr4[1])
        battleplace.unshift(tr4)
        t4picked = true
    elsif randplace == 4 && t5picked == false
        $boardplace.unshift(tr5[1])
        battleplace.unshift(tr5)
        t5picked = true
    elsif randplace == 5 && t6picked == false
        $boardplace.unshift(tr6[1])
        battleplace.unshift(tr6)
        t6picked = true
    elsif randplace == 6 && t7picked == false
        $boardplace.unshift(tr7[1])
        battleplace.unshift(tr7)
        t7picked = true
    end 
  end until $boardplace.length == 7

  $battleplace0 = battleplace[0]
  $battleplace1 = battleplace[1]
  $battleplace2 = battleplace[2] 
  $battleplace3 = battleplace[3] 
  $battleplace4 = battleplace[4]
  $battleplace5 = battleplace[5]
  $battleplace6 = battleplace[6]
end

# --------------------------- Semi Finals Setup ----------------------------- 

def pbtournamentSemiSetup
  
  $prelimRound = false
  $semiRound = true
  $finalRound = false

  b2gen = rand(2)
  if b2gen == 0
    $battleplace0 = $battleplace1
    $boardplace[0] = $battleplace0[1]
    $battleplace2.push("lost")
  elsif b2gen == 1
    $battleplace0 = $battleplace2
    $boardplace[0] = $battleplace0[1]
    $battleplace1.push("lost")
  end

  b3gen = rand(2)
  if b3gen == 0
    $battleplace1 = $battleplace3
    $boardplace[1] = $battleplace1[1]
    $battleplace4.push("lost")
  elsif b3gen == 1
    $battleplace1 = $battleplace4
    $boardplace[1] = $battleplace1[1]
    $battleplace3.push("lost")
  end
  
  b4gen = rand(2)
  if b4gen == 0
    $battleplace2 = $battleplace5
    $boardplace[2] = $battleplace2[1]
    $battleplace6.push("lost")
  elsif b4gen == 1
    $battleplace2 = $battleplace6
    $boardplace[2] = $battleplace2[1]
    $battleplace5.push("lost")
  end
end
  
# ------------------------- Finals Setup ---------------------------------

def pbtournamentFinalsSetup
  
  $prelimRound = false
  $semiRound = false
  $finalRound = true

  b2gen = rand(2)
  if b2gen == 0
    $battleplace0 = $battleplace1
    $boardplace[0] = $battleplace0[1]
  elsif b2gen == 1
    $battleplace0 = $battleplace2
    $boardplace[0] = $battleplace0[1]
  end
end

#------------------------Tournament Board/Announcer----------------------------

def pbTourneyBoard

  if $prelimRound == true  
    Kernel.pbMessage(_INTL("Current standings for the Glacier Cup"))
    Kernel.pbMessage(_INTL("Preliminary Round 1"))
    Kernel.pbMessage(_INTL("\\PN vs. #{$boardplace[0]}"))
    Kernel.pbMessage(_INTL("Preliminary Round 2"))
    Kernel.pbMessage(_INTL("#{$boardplace[1]} vs. #{$boardplace[2]}"))
    Kernel.pbMessage(_INTL("Preliminary Round 3"))
    Kernel.pbMessage(_INTL("#{$boardplace[3]} vs. #{$boardplace[4]}"))
    Kernel.pbMessage(_INTL("Preliminary Round 4"))
    Kernel.pbMessage(_INTL("#{$boardplace[5]} vs. #{$boardplace[6]}"))
  
  elsif $semiRound == true
    Kernel.pbMessage(_INTL("Current standings for the Glacier Cup"))
    Kernel.pbMessage(_INTL("Semi-finals Round 1"))
    Kernel.pbMessage(_INTL("\\PN vs. #{$boardplace[0]}"))
    Kernel.pbMessage(_INTL("Semi-finals Round 2"))
    Kernel.pbMessage(_INTL("#{$boardplace[1]} vs. #{$boardplace[2]}"))
  
  elsif $finalRound == true
    Kernel.pbMessage(_INTL("Current standings for the Glacier Cup"))
    Kernel.pbMessage(_INTL("Finals"))
    Kernel.pbMessage(_INTL("\\PN vs. #{$boardplace[0]}"))

  else 
    Kernel.pbMessage(_INTL("Sorry no tournament standings have been posted"))
  end
end

def currentOpponentName
  Kernel.pbMessage(_INTL("#{$boardplace[0]}"))
end

#----------------------- Challenger Sprites -----------------------------

def fcGraphicID
  if $boardplace[0] == "Misty" 
    $game_switches[55] = true
  elsif $boardplace[0] == "Josh (Northshore Finalist)" 
    $game_switches[56] = true
  elsif $boardplace[0] == "Oca (Wilds Cup Finalist)" 
    $game_switches[57] = true
  elsif $boardplace[0] == "Isidore"
    $game_switches[59] = true
  elsif $boardplace[0] == "Pryce"
    $game_switches[60] = true
  elsif $boardplace[0] == "Candice"
    $game_switches[61] = true
  elsif $boardplace[0] == "Mark (Village Cup Champ)"
    $game_switches[62] = true 
  end
end

def fcGraphicRefresh
    $game_switches[55] = false
    $game_switches[56] = false
    $game_switches[57] = false
    $game_switches[59] = false
    $game_switches[60] = false
    $game_switches[61] = false
    $game_switches[62] = false
end

# ----------------------- Overworld Speech ------------------------------

def alSpeech
  if $boardplace[0] == "Misty" 
    Kernel.pbMessage(_INTL("Misty."))
    Kernel.pbMessage(_INTL("Hehe..."))
    Kernel.pbMessage(_INTL("Hoho..."))
    Kernel.pbMessage(_INTL("Right sorry...Misty"))
    Kernel.pbMessage(_INTL("Part of her team consists of a Starmie and a Milotit-..tic."))
    Kernel.pbMessage(_INTL("Ahem. I'd watch out for her Starmie's Thunderbolt, she can fry anyone of"))
    Kernel.pbMessage(_INTL("your water types you bring into the fight."))
  elsif $boardplace[0] == "Isidore" 
    Kernel.pbMessage(_INTL("Isidore."))
    Kernel.pbMessage(_INTL("This young man was smart enough to bring a Blastoise with"))
    Kernel.pbMessage(_INTL("Brick Break. You may ask, how is this smart? Well if you knew"))
    Kernel.pbMessage(_INTL("anything about how types work kid, you'd know not to let any"))
    Kernel.pbMessage(_INTL("ice types get fisted."))
  elsif $boardplace[0] == "Pryce"
    Kernel.pbMessage(_INTL("Pryce."))
    Kernel.pbMessage(_INTL("This old fart's biggest threat is Mamoswine..."))
    Kernel.pbMessage(_INTL("No kid not that, I mean his Mamoswine. He's a physical"))
    Kernel.pbMessage(_INTL("attack monstrosity to any ice type that deals with him."))
   elsif $boardplace[0] == "Candice"
    Kernel.pbMessage(_INTL("Candice."))
    Kernel.pbMessage(_INTL("Don't let her looks deceive you kid, she'll tear you a new one"))
    Kernel.pbMessage(_INTL("if you're not careful. She's going to try some new meta mumbo jumbo,"))
    Kernel.pbMessage(_INTL("to be honest, I don't quite understand with her Froslass... so ummm"))
    Kernel.pbMessage(_INTL("good luck kid, let me know how it goes."))
   elsif $boardplace[0] == "Mark (Village Cup Champ)"
    Kernel.pbMessage(_INTL("Mark."))
    Kernel.pbMessage(_INTL("Now this guy is an arrogant prick."))
    Kernel.pbMessage(_INTL("..."))
    Kernel.pbMessage(_INTL("...What?"))
    Kernel.pbMessage(_INTL("Oh right, he is more than likely going to use his Kingdra"))
    Kernel.pbMessage(_INTL("to take advantage of his type weaknesses. I'd make like the"))
    Kernel.pbMessage(_INTL("mob and find a way around it."))
   elsif $boardplace[0] == "Oca (Wilds Cup Finalist)"
    Kernel.pbMessage(_INTL("Oca."))
    Kernel.pbMessage(_INTL("Hmmm a local from the village."))
    Kernel.pbMessage(_INTL("The only strategic advice that I can give you is that he"))
    Kernel.pbMessage(_INTL("uses a Weavile, Gastrodon and Mamoswine."))
    Kernel.pbMessage(_INTL("Moves? Sorry kid, to tell ya the truth I kinda dozed off"))
    Kernel.pbMessage(_INTL("watching him battle. But you have nothing to worry about trust me haha."))
   elsif $boardplace[0] == "Josh (Northshore Finalist)"
    Kernel.pbMessage(_INTL("Josh."))
    Kernel.pbMessage(_INTL("Now this guy, talk about a starter tool haha. His team comprises"))
    Kernel.pbMessage(_INTL("of only starters. However theres no telling what starters"))
    Kernel.pbMessage(_INTL("he's going to use. But I have faith in ya kid."))
  end
end

def gcMistySpeech
  if $boardplace[0] == "Misty" && $prelimRound == true 
    Kernel.pbMessage(_INTL("Hey are you \\PN?"))
    Kernel.pbMessage(_INTL("It looks like we're battling in the preliminaries, good luck."))
  elsif $boardplace[0] != "Misty" && $prelimRound == true
    Kernel.pbMessage(_INTL("Hey are you \\PN?"))
    Kernel.pbMessage(_INTL("Good luck with your battle, mine will be a piece of cake.")) 
  elsif $boardplace[0] == "Misty" && $semiRound == true 
    Kernel.pbMessage(_INTL("Hey \\PN!"))
    Kernel.pbMessage(_INTL("It looks like we're battling in the semifinals, good luck."))
  elsif $boardplace[0] != "Misty" && $semiRound == true
    Kernel.pbMessage(_INTL("Hey \\PN!"))
    Kernel.pbMessage(_INTL("Looks like you made it the semi finals, good luck!"))
  elsif $boardplace[0] == "Misty" && $finalRound == true
    Kernel.pbMessage(_INTL("Hey \\PN!"))
    Kernel.pbMessage(_INTL("Prepare yourself because i'm not going easy on you haha!"))
  elsif $boardplace[0] != "Misty" && $finalRound == true
    Kernel.pbMessage(_INTL("Hey \\PN!"))
    Kernel.pbMessage(_INTL("Congrats on making it all the way! I'll be rooting for you!"))
  end
end

#-----------------------------------------------------------------------
# --------------------- Alternative Battle Method ----------------------
#-----------------------------------------------------------------------

# Copied from pbTrainerBattle method and change arguments to array. 

def pbTrainerBattleAlt(battleplaceArr)
  
  trainerid = battleplaceArr[0]
  trainername = battleplaceArr[1] 
  endspeech = battleplaceArr[2]
  doublebattle = battleplaceArr[3]
  trainerparty = battleplaceArr[4]
  canlose = battleplaceArr[5]
  variable = battleplaceArr[6]
                        
                    
  if $Trainer.pokemonCount==0
    Kernel.pbMessage(_INTL("SKIPPING BATTLE...")) if $DEBUG
    return false
  end
  if !$PokemonTemp.waitingTrainer && $Trainer.ablePokemonCount>1 &&
     pbMapInterpreterRunning?
    thisEvent=pbMapInterpreter.get_character(0)
    triggeredEvents=$game_player.pbTriggeredTrainerEvents([2],false)
    otherEvent=[]
    for i in triggeredEvents
      if i.id!=thisEvent.id && !$game_self_switches[[$game_map.map_id,i.id,"A"]]
        otherEvent.push(i)
      end
    end
    if otherEvent.length==1
      trainer=pbLoadTrainer(trainerid,trainername,trainerparty)
      Events.onTrainerPartyLoad.trigger(nil,trainer)
      if !trainer
        pbMissingTrainer(trainerid,trainername,trainerparty)
        return false
      end
      if trainer[2].length<=6 # 3
        $PokemonTemp.waitingTrainer=[trainer,thisEvent.id,endspeech]
        return false
      end
    end
  end
  trainer=pbLoadTrainer(trainerid,trainername,trainerparty)
  Events.onTrainerPartyLoad.trigger(nil,trainer)
  if !trainer
    pbMissingTrainer(trainerid,trainername,trainerparty)
    return false
  end
  if $PokemonGlobal.partner && ($PokemonTemp.waitingTrainer || doublebattle)
    othertrainer=PokeBattle_Trainer.new(
       $PokemonGlobal.partner[1],$PokemonGlobal.partner[0])
    othertrainer.id=$PokemonGlobal.partner[2]
    othertrainer.party=$PokemonGlobal.partner[3]
    playerparty=[]
    for i in 0...$Trainer.party.length
      playerparty[i]=$Trainer.party[i]
    end
    for i in 0...othertrainer.party.length
      playerparty[6+i]=othertrainer.party[i]
    end
    fullparty1=true
    playertrainer=[$Trainer,othertrainer]
    doublebattle=true
  else
    playerparty=$Trainer.party
    playertrainer=$Trainer
    fullparty1=false
  end
  if $PokemonTemp.waitingTrainer
    combinedParty=[]
    fullparty2=false
    if false
      if $PokemonTemp.waitingTrainer[0][2].length>3
        raise _INTL("Opponent 1's party has more than three Pokémon, which is not allowed")
      end
      if trainer[2].length>3
        raise _INTL("Opponent 2's party has more than three Pokémon, which is not allowed")
      end
    elsif $PokemonTemp.waitingTrainer[0][2].length>3 || trainer[2].length>3
      for i in 0...$PokemonTemp.waitingTrainer[0][2].length
        combinedParty[i]=$PokemonTemp.waitingTrainer[0][2][i]
      end
      for i in 0...trainer[2].length
        combinedParty[6+i]=trainer[2][i]
      end
      fullparty2=true
    else
      for i in 0...$PokemonTemp.waitingTrainer[0][2].length
        combinedParty[i]=$PokemonTemp.waitingTrainer[0][2][i]
      end
      for i in 0...trainer[2].length
        combinedParty[3+i]=trainer[2][i]
      end
      fullparty2=false
    end
    scene=pbNewBattleScene
    battle=PokeBattle_Battle.new(scene,playerparty,combinedParty,playertrainer,
       [$PokemonTemp.waitingTrainer[0][0],trainer[0]])
    trainerbgm=pbGetTrainerBattleBGM(
       [$PokemonTemp.waitingTrainer[0][0],trainer[0]])
    battle.fullparty1=fullparty1
    battle.fullparty2=fullparty2
    battle.doublebattle=battle.pbDoubleBattleAllowed?()
    battle.endspeech=$PokemonTemp.waitingTrainer[2]
    battle.endspeech2=endspeech
    battle.items=[$PokemonTemp.waitingTrainer[0][1],trainer[1]]
  else
    scene=pbNewBattleScene
    battle=PokeBattle_Battle.new(scene,playerparty,trainer[2],playertrainer,trainer[0])
    battle.fullparty1=fullparty1
    battle.doublebattle=doublebattle ? battle.pbDoubleBattleAllowed?() : false
    battle.endspeech=endspeech
    battle.items=trainer[1]
    trainerbgm=pbGetTrainerBattleBGM(trainer[0])
  end
  if Input.press?(Input::CTRL) && $DEBUG
    Kernel.pbMessage(_INTL("SKIPPING BATTLE..."))
    Kernel.pbMessage(_INTL("AFTER LOSING..."))
    Kernel.pbMessage(battle.endspeech)
    Kernel.pbMessage(battle.endspeech2) if battle.endspeech2
    if $PokemonTemp.waitingTrainer
      pbMapInterpreter.pbSetSelfSwitch($PokemonTemp.waitingTrainer[1],"A",true)
      $PokemonTemp.waitingTrainer=nil
    end
    return true
  end
  Events.onStartBattle.trigger(nil,nil)
  battle.internalbattle=true
  pbPrepareBattle(battle)
  restorebgm=true
  decision=0
  Audio.me_stop
  pbBattleAnimation(trainerbgm,trainer[0].trainertype,trainer[0].name) { 
     pbSceneStandby {
        decision=battle.pbStartBattle(canlose)
     }
     for i in $Trainer.party; (i.makeUnmega rescue nil); (i.makeUnprimal rescue nil); end
     if $PokemonGlobal.partner
       pbHealAll
       for i in $PokemonGlobal.partner[3]
         i.heal
         i.makeUnmega rescue nil
         i.makeUnprimal rescue nil
       end
     end
     if decision==2 || decision==5
       if canlose
         for i in $Trainer.party; i.heal; end
         for i in 0...10
           Graphics.update
         end
#       else
#         $game_system.bgm_unpause
#         $game_system.bgs_unpause
#         Kernel.pbStartOver
       end
     end
     Events.onEndBattle.trigger(nil,decision,canlose)
     if decision==1
       if $PokemonTemp.waitingTrainer
         pbMapInterpreter.pbSetSelfSwitch($PokemonTemp.waitingTrainer[1],"A",true)
       end
     end
  }
  Input.update
  pbSet(variable,decision)
  $PokemonTemp.waitingTrainer=nil
  return (decision==1)
end