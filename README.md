## A High Stakes Investigation (excercise)

### Scenario

You have just been hired by Lucky Duck Casino as a security analyst.

 - Lucky Duck has lost a significant amount of money on the roulette tables over the last month.

 - The largest losses occurred on March 10, 12, and 15.

 - Your manager believes there is a player working with a Lucky Duck dealer to steal money at the roulette tables.

 - The casino has a large database with data on wins and losses, player analysis, and dealer schedules.

- You are tasked with navigating, modifying, and analyzing these data files to gather evidence on the rogue player and dealer.

 - You will prepare several evidence files to assist the prosecution.

 - You must work quickly as Lucky Duck can't afford any more losses.







### Instructions 

Use your command-line skills to uncover the identities of the rogue casino player and dealer colluding to scam Lucky Duck out of thousands of dollars. 

After your investigation, you will provide a summary of your findings to the casino. 

#### Step 1: Investigation Preparation

Your first task is to set up directories to prepare for your investigation.

1. Begin by making a single directory titled `Lucky_Duck_Investigations`.
         
       mkdir Lucky_Duck_Investigation

2. In this directory, create a directory for this specific investigation titled `Roulette_Loss_Investigation`.

       mkdir Roulette_loss_Investigation

3. In `Roulette_Loss_Investigation`, create the following directories:

    - `Player_Analysis` to investigate the casino player.
    - `Dealer_Analysis` to investigate the dealers.
    - `Player_Dealer_Correlation` to summarize your findings of the collusion.

          mkdir Player_Analysis Dealer_Analysis Player_Dealer_Correlation
               

4. Create empty files called `Notes_<Directory Name>` under each subdirectory to store investigation notes.

    - For example: `Notes_Player_Analysis`

Player Notes
        
          cd Player_Analysis/
          touch Notes_Player_Analysis.txt
         
Dealer Notes
  
          cd Dealer_Analysis/
          touch Notes_Dealer_Schedule.txt
          
Player Dealer Correlation
         
          cd Player_Dealer_Correlation/
          touch Notes_Dealer_Correlation.txt
          
 - Run `ls -R` to ensure that your files are listed correctly in each directory.
 ![image4](https://user-images.githubusercontent.com/115432675/211075194-46024cb4-34b0-43c5-937a-44d1a6d3ba21.png)

#### Step 2: Gathering Evidence

Your next task is to move evidence from the specific days that Lucky Duck experienced heavy losses at the roulette tables.

1. Navigate to the directory where you created the `Lucky_Duck_Investigations` directory and run the following command to set up the evidence files:

   - `wget "https://drive.google.com/uc?id=1ZLY_fuFu3wz7tOlxf-GUrnvp3htuGKSa" -O 3-HW-setup-evidence && chmod +x ./3-HW-setup-evidence && ./3-HW-setup-evidence`

      ![image17](https://user-images.githubusercontent.com/115432675/211077127-c0b03e88-882f-4d63-88b2-9db5cc06b94a.png)

   After running this command your current directory should have the following subdirectories:

      - `Dealer_Schedules_0310`: Contains the dealer schedules.
      - `Lucky_Duck_Investigations`: Contains the investigation directories and notes files you created.
      - `Roulette_Player_WinLoss_0310`: Contains the data for player wins and losses.


2. The `Dealer_Schedules_0310` and `Roulette_Player_WinLoss_0310` directories contain the dealer schedules and win/loss player data from the roulette tables during the week of March 10.

     -  Since the losses occurred on March 10, 12, and 15, move the schedules for those days into the directory `Dealer_Analysis`.
    
            mv 0310_Dealer_schedule.txt 0312_Dealer_schedule.txt 0315_Dealer_schedule.txt ../Roulette_loss_Investigation/Dealer_Analysis
     
    - Move the files for those days into the directory `Player_Analysis`.

          mv 0310_win_loss_player_data.txt 0312_win_loss_player_data.txt 0315_win_loss_player_data.txt ../Roulette_loss_Investigation/Player_Analysis/
                      
          

#### Step 3: Correlating the Evidence

Your next task is to correlate the large losses from the roulette tables with the dealer schedule. This will help you determine which dealer and player are colluding to steal money from Lucky Duck.

  **Note:** Winnings for Lucky Duck Casino are indicated with a positive number and losses are indicated with a negative number.

Complete the player analysis.
  1. Navigate to the `Player_Analysis` directory.

  2. Use `grep` to isolate all of the losses that occurred on March 10, 12, and 15.
                
         cat 0310_win_loss_player_data.txt 0312_win_loss_player_data.txt 0315_win_loss_player_data.txt | grep -
         
   ![image13](https://user-images.githubusercontent.com/115432675/211083562-d0dfbeff-1865-4163-900c-c8f7d9b2d29f.png)

  3. Place those results in a file called `Roulette_Losses`.

         cat 0310_win_loss_player_data.txt 0312_win_loss_player_data.txt 0315_win_loss_player_data.txt | grep - > Roulette_Losses.txt
        - `cat Roulette_Losses.txt` to check the file that you've just created

   ![image8](https://user-images.githubusercontent.com/115432675/211084113-b6562271-ed49-4ed0-ab48-490ff99ccc9f.png)

  4. Preview the file `Roulette_Losses` and analyze the data.

      - Record in the `Notes_Player_Analysis` file:

        - The times the losses occurred on each day.
        - If there is a certain player that was playing during each of those times.
        - The total count of times this player was playing.
          - **Hint:** Use the `wc` command to find this value.

              
                grep “-” Roulette_Losses.txt | awk -F" " '{print $1" "$2}' >> Notes_Player_Analysis.txt
                
               ![image10](https://user-images.githubusercontent.com/115432675/211085072-b6769261-dbd7-4288-be6e-e13cb900ebce.png) 
      
     - To find the common player let's use `grep` to isolate players and find who appears the most:
 
           cat Roulette_Losses.txt | grep "Mylie Schmidt" Roulette_Losses.txt
           
          ![image15](https://user-images.githubusercontent.com/115432675/211088646-52d992cb-8838-4560-9b5e-a5baabb273a3.png)

           
     - Next we'll find how many times this person has appeared in the losses:
     
    cat Roulette_Losses.txt | grep "Mylie Schmidt" Roulette_Losses.txt | wc -l  
    
   ![image3](https://user-images.githubusercontent.com/115432675/211089145-35f958a8-1aa9-4e14-aea9-fab83c468f38.png)
   
   - Now we can move these Notes_Player_Analysis.txt file. You can eith use `>>` to move the commands in to the file or `nano Notes_Player_Analysis.txt` to make edit the text file `Notes_Player_Analysis.txt`. Next `cat Notes_PLayer_Analysis.txt` to see your file once you've added the notes.
  
![image19](https://user-images.githubusercontent.com/115432675/211090137-58c4a684-7536-4f20-8ba5-853e3a8ef4be.png)

    
       
Complete the dealer analysis. 
  1. Navigate to the `Dealer_Analysis` directory.

  2. This file contains the dealer schedules for the various Lucky Duck casino games: Blackjack, Roulette, and Texas Hold 'Em.

      - Preview the schedule to view the format and to understand how the data is separated.

            head -n 10 0310_Dealer_schedule.txt  0315_Dealer_schedule.txt 0312_Dealer_schedule.txt

  3. Using your findings from the player analysis, create a separate script to look at each day and time that you determined losses occurred. Use `awk`, `pipes`, and `grep` to isolate out the following four fields:

      - Time
      - a.m./p.m.
      - First name of roulette dealer
      - Last name of roulette dealer


      For example, if a loss occurred on March 10 at 2 p.m., you would write one script to find the roulette dealer who was working at that specific day and time.

      - **Hint:** You will have many scripts, but only a small change is required for each script.

    cat 0310_Dealer_schedule.txt | awk -F" " '{print $1, $2, $5,$6}'| grep '05:00:00 AM' 
    
   ![image9](https://user-images.githubusercontent.com/115432675/211092025-8e6bbac2-1de4-4c9b-9223-a4e122910cb5.png)

  5. Run all of the scripts and append those results to a file called `Dealers_working_during_losses`.

    cat 0310_Dealer_schedule.txt | awk -F" " '{print $1, $2, $5,$6}'| grep '05:00:00 AM' >> Dealers_working_during_losses.txt 
    cat 0310_Dealer_schedule.txt | awk -F" " '{print $1, $2, $5,$6}'| grep '08:00:00 AM' >> Dealers_working_during_losses.txt 
    cat 0310_Dealer_schedule.txt | awk -F" " '{print $1, $2, $5,$6}'| grep '02:00:00 PM' >> Dealers_working_during_losses.txt 
    cat 0310_Dealer_schedule.txt | awk -F" " '{print $1, $2, $5,$6}'| grep '08:00:00 PM' >> Dealers_working_during_losses.txt
    cat 0310_Dealer_schedule.txt | awk -F" " '{print $1, $2, $5,$6}'| grep '11:00:00 PM' >> Dealers_working_during_losses.txt
    cat 0312_Dealer_schedule.txt | awk -F" " '{print $1, $2, $5,$6}'| grep '05:00:00 AM' >> Dealers_working_during_losses.txt
    cat 0312_Dealer_schedule.txt | awk -F" " '{print $1, $2, $5,$6}'| grep '08:00:00 AM' >> Dealers_working_during_losses.txt
    cat 0312_Dealer_schedule.txt | awk -F" " '{print $1, $2, $5,$6}'| grep '02:00:00 PM' >> Dealers_working_during_losses.txt
    cat 0312_Dealer_schedule.txt | awk -F" " '{print $1, $2, $5,$6}'| grep '08:00:00 PM' >> Dealers_working_during_losses.txt
    cat 0312_Dealer_schedule.txt | awk -F" " '{print $1, $2, $5,$6}'| grep '11:00:00 PM' >> Dealers_working_during_losses.txt
    cat 0315_Dealer_schedule.txt | awk -F" " '{print $1, $2, $5,$6}'| grep '05:00:00 AM' >> Dealers_working_during_losses.txt
    cat 0315_Dealer_schedule.txt | awk -F" " '{print $1, $2, $5,$6}'| grep '08:00:00 AM' >> Dealers_working_during_losses.txt
    cat 0315_Dealer_schedule.txt | awk -F" " '{print $1, $2, $5,$6}'| grep '02:00:00 PM' >> Dealers_working_during_losses.txt


  6. Preview your file `Dealers_working_during_losses` and analyze the data.
  
      - Record in the `Notes_Dealer_Analysis` file:

        - The primary dealer working at the times where losses occurred.

        - How many times the dealer worked when major losses occurred.

               echo "Total number of times this dealer was at the table during a loss:" >> Dealers_working_during_losses.txt
               
               grep -i "billy jones" Dealers_working_during_losses.txt | wc -l >> Dealers_working_during_losse
               
               cat Dealers_working_during_losses.txt
               
             ![image22](https://user-images.githubusercontent.com/115432675/211093544-06ec5ce8-d6b1-44a7-91bb-67071231c196.png)

3. Complete the player/employee correlation. 

   - In the notes file of the `Player_Dealer_Correlation` directory, add a summary of your findings noting the player and dealer you believe are colluding to scam Lucky Duck.

          nano Notes_Player_Dealer_Correlation.txt
    
    
    - Make sure to document your specific reasons for this finding.
    - Include a note on your findings:
    ![image12](https://user-images.githubusercontent.com/115432675/211094397-7c7ac52b-116b-4903-bd69-ec6e5e736115.png)   



#### Step 4: Scripting Your Tasks

You manager is impressed with the work you have done so far on the investigation.  

 They tasked you with building a shell script that can easily analyze future employee schedules. They will use this to determine which employee was working at a specific time in the case of future losses.

Complete the following tasks:

1. Remain in the `Dealer_Analysis` directory.  Develop a shell script called `roulette_dealer_finder_by_time.sh` that can analyze the employee schedule to easily find the roulette dealer at a specific time.

      **Hint:** You will be using a script similar to the one you created for the dealer analysis step, but you will not output the results into a file.

    - Design the shell script to accept the following two arguments:
      - One for the date (four digits)
      - One for the time

     **Note:** The argument should be able to accept a.m. or p.m.
     
       nano roulette_dealer_finder_by_time.sh 
       
      -Be sure to use `#!/bin/bash` at the top of your script:
      
        cat $1_Dealer_schedule.txt | awk -F" " '{print $1, $2, $5, $6}' | grep "$2"

      ![image2](https://user-images.githubusercontent.com/115432675/211095963-355865f4-68c1-4f2f-b71d-c08b331c2dfe.png)

3. Test your script on the schedules to confirm it outputs the correct dealer at the time specified.
 
       sh roulette_dealer_finder_by_time.sh 0310 '02:00:00 PM'

      ![image20](https://user-images.githubusercontent.com/115432675/211096670-94a9cba4-fecd-48a7-ace2-816fa01ef328.png)


#### Bonus

- In case there is future fraud on the other Lucky Duck games, create a shell script called `roulette_dealer_finder_by_time_and_game.sh` that has the three following arguments:

   - Specific time
   - Specific date
   - Casino game being played

  **Hint:** The argument does not need to name the specific casino game.
   - Make the script
         
         nano roulettel_dealer_finder_by_time_and_game.sh
      
   - Make the modification to the script by changing the arguments `$5, $6` from the previous script to `$3, $4`:
  
         cat $1_Dealer_schedule.txt | awk -F" " '{print $1, $2, '$3','$4' }'| grep "$2"   
         
   - When running the script you will need to specify each argument using `$`
   
          sh roulette_dealer_finder_by_time_and_game.sh 0310 '02:00:00 PM' '$3' '$4'
          sh roulette_dealer_finder_by_time_and_game.sh 0310 '02:00:00 PM' '$5' '$6'
          sh roulette_dealer_finder_by_time_and_game.sh 0310 '02:00:00 PM' '$7' '$8'
          
        ![image1](https://user-images.githubusercontent.com/115432675/211097805-b6af0856-4c54-4b28-86ac-a664da584657.png)
          
   

### Submission Guidelines

- Move the following to the `Player_Dealer_Correlation` directory:
  - All note files
  - Evidence files:
    - `Roulette_Losses`
    - `Dealers_working_during_losses`
  - Shell script(s)

- Compress the `Player_Dealer_Correlation` folder to a zip file and submit it.

![Screenshot 2023-01-06 161350](https://user-images.githubusercontent.com/115432675/211101391-574b39f3-5d79-481f-b900-d62d53070228.png)

  ![Screenshot 2023-01-06 161019](https://user-images.githubusercontent.com/115432675/211100849-3b5a1a3d-a064-4672-9b9f-3b64f400e4eb.png)
  
  
