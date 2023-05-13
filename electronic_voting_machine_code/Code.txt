#include<LiquidCrystal.h>
LiquidCrystal lcd(13, 12, 11, 10, 9, 8); //Create an instance of the LiquidCrystal class with the specified pin numbers

//Define the pin numbers for switch
#define S1 7
#define S2 6
#define S3 5
#define S4 4
#define S5 3

//Initialize the variable to store the number of votes
int vote1 = 0;
int vote2 = 0;
int vote3 = 0;
int vote4 = 0;
void setup()
{
  // Set the mode of the pins S1-S5 as input
  pinMode(S1, INPUT);
  pinMode(S2, INPUT);
  pinMode(S3, INPUT);
  pinMode(S4, INPUT);
  pinMode(S5, INPUT);

  // Initialize the LiquidCrystal library with the specified pin numbers  
  lcd.begin(16, 2);
  
  // Display a message on the first line of the LCD  
  lcd.print("Electronic ");

  // Move the cursor to the second line of the LCD  
  lcd.setCursor(0, 1);

  // Display a message on the second line of the LCD  
  lcd.print(" Voting Machine ");

  // Wait for 4 seconds  
  delay(4000);

  // Set the pins S1-S5 to HIGH (turn off the LEDs connected to them)
  digitalWrite(S1, HIGH);
  digitalWrite(S2, HIGH);
  digitalWrite(S3, HIGH);
  digitalWrite(S4, HIGH);
  digitalWrite(S5, HIGH);

  // Clear the LCD display  
  lcd.clear();

  // Display the names of the candidates on the LCD
  lcd.setCursor(1, 0);
  lcd.print("A");
  lcd.setCursor(5, 0);
  lcd.print("B");
  lcd.setCursor(9, 0);
  lcd.print("C");
  lcd.setCursor(13, 0);
  lcd.print("D");
}

void loop()
{
  // Display candidate names and current vote counts
  lcd.setCursor(1, 0);
  lcd.print("A");
  lcd.setCursor(1, 1);
  lcd.print(vote1);
  lcd.setCursor(5, 0);
  lcd.print("B");
  lcd.setCursor(5, 1);
  lcd.print(vote2);
  lcd.setCursor(9, 0);
  lcd.print("C");
  lcd.setCursor(9, 1);
  lcd.print(vote3);
  lcd.setCursor(13, 0);
  lcd.print("D");
  lcd.setCursor(13, 1);
  lcd.print(vote4);

  // Update vote counts if a button is pressed
  if (digitalRead(S1) == 0)
    vote1++;
  while (digitalRead(S1) == 0);
  if (digitalRead(S2) == 0)
    vote2++;
  while (digitalRead(S2) == 0);
  if (digitalRead(S3) == 0)
    vote3++;
  while (digitalRead(S3) == 0);
  if (digitalRead(S4) == 0)
    vote4++;
  while (digitalRead(S4) == 0);

  // If the "end voting" button is pressed
  if (digitalRead(S5) == 0)
  {
    // Calculate total votes
    int vote = vote1 + vote2 + vote3 + vote4;
    if (vote)
    {
      // Determine the winner based on the highest number of votes        
      if ((vote1 > vote2 && vote1 > vote3 && vote1 > vote4))
      {
        lcd.clear();
        lcd.print("Ahsan is Winner");
        delay(3000);
        lcd.clear();
      }
      else if ((vote2 > vote1 && vote2 > vote3 && vote2 > vote4))
      {
        lcd.clear();
        lcd.print("Basit is Winner");
        delay(3000);
        lcd.clear();
      }
      else if ((vote3 > vote1 && vote3 > vote2 && vote3 > vote4))
      {
        lcd.clear();
        lcd.print("Moazam is Winner");
        delay(3000);
        lcd.clear();
      }
      else if (vote4 > vote1 && vote4 > vote2 && vote4 > vote3)
      {
        lcd.setCursor(0, 0);
        lcd.clear();
        lcd.print("Danial is Winner");
        delay(3000);
        lcd.clear();
      }

      else if (vote4 > vote1 && vote4 > vote2 && vote4 > vote3)
      {
        lcd.setCursor(0, 0);
        lcd.clear();
        lcd.print("Danial is Winner");
        delay(3000);
        lcd.clear();
      }

      // If there is a tie or no votes, display a message indicating no result      
      else
      {
        lcd.clear();
        lcd.print(" Tie Up Or ");
        lcd.setCursor(0, 1);
        lcd.print(" No Result ");
        delay(3000);
        lcd.clear();
      }

    }
    else
    {
      // Display message indicating there were no votes      
      lcd.clear();
      lcd.print("No Voting....");
      delay(3000);
      lcd.clear();
    }
    // Reset all vote counts and clear the LCD    
    vote1 = 0; vote2 = 0; vote3 = 0; vote4 = 0, vote = 0;
    lcd.clear();
  }
}
