import java.util.*;
class SinglePlayer
{
    static String user_team = "";
    static String op_team = "";
    static String player_team[] = new String[]{"India", "Australia", "England", "New Zealand", "Pakistan"};
    static String opponent_team[] = new String[]{"India", "Australia", "England", "New Zealand", "Pakistan"};
    static String extras[] = new String[5];
    static String selected_team[] = new String[11];

    static String india_default[] = new String[]{"Shikhar Dhawan" ,"Rohit Sharma" ,"Virat Kohli", "Shreyas Iyer", "KL Rahul", "Ajinkya Rahane", "Mayank Agarwal",
                                                 "Rishabh Pant", "Hardik Pandya", "MS Dhoni", "Ravindra Jadeja", "Yuzvendra Chahal", "Mohammed Shami", "Jasprit Bumrah",
                                                 "Bhuvneshwar Kumar", "Kuldeep Yadav"};
    static int india_skill[] = new int[]{88, 92, 99, 84, 85, 88, 81, 87, 92, 100, 90, 60, 70, 55, 68, 62};

    static String australia_default[] = new String[]{"David Warner", "Aaron Finch", "Steve Smith", "Marcus Stoinis", "Glenn Maxwell", "Marnus Labuchagne", "Mathew Wade",
                                                     "D'Arcy Short", "Alex Carey", "Ashton Turner", "Josh Hazelwood", "Pat Cummins", "Nathan Lyon", "Mitchell Starc",
                                                     "Adam Zampa", "Kane Richardson"};
    static int australia_skill[] = new int[]{96, 92, 98, 90, 92, 88, 81, 80, 89, 78, 61, 52, 65, 68, 54, 60};

    static String england_default[] = new String[]{"Alex Hales", "Jason Roy", "Eoin Morgan", "Joe Root", "Moeen Ali", "Jos Butler", "Ben Stokes", "Tom Banton",
                                                   "Tom Curran", "Jonny Bairstow", "Jofra Archer", "Chris Woakes", "Sam Curran", "Jack Leach", "Liam Dawson",
                                                   "Mark Wood"};
    static int england_skill[] = new int[]{86, 89, 95, 97, 84, 88, 96, 84, 81, 85, 74, 76, 60, 52, 58, 53};

    static String newZealand_default[] = new String[]{"Martin Guptill", "Henry Nicholls", "Ross Taylor", "Kane Williamson", "Tom Latham", "Colin de Grandhomme",
                                                      "Jimmy Neesham", "Mitchell Santner", "Colin Munro", "Tom Bruce", "Matt Henry", "Todd Astle", "Kyle Jamieson",
                                                      "Tim Southee", "Scott Kuggeleijn", "Ish Sodhi"};
    static int newZealand_skill[] = new int[]{93, 87, 95, 91, 82, 92, 90, 89, 84, 72, 67, 62, 55, 69, 54, 59};

    static String pakistan_default[] = new String[]{"Fakhar Zaman", "Asif Ali", "Imam-ul-Haq", "Mohammad Hafiz", "Babar Azam", "Faheem Ashraf", "Fawad Alam",
                                                    "Haris Sohail", "Mohammad Amir", "Naseem Shah", "Shaheen Afridi", "Sarfaraz Ahmed", "Azhar Ali", "Yasir Shah",
                                                    "Mohammad Abbas", "Imran Khan"};
    static int pakistan_skill[] = new int[]{81, 83, 88, 84, 90, 77, 74, 87, 48, 51, 52, 72, 52, 55, 58, 52};

    public static String[] getPlayingXI(String name)
    {
        return selected_team;
    }

    public void filter(String name)
    {
        if (name.equals("India"))
        {
            int count = 0;
            String temp = "";
            for (int i = 0; i < india_default.length - 1; i++)
            {
                if (india_default[i].equals("XXX"))
                {
                    count++;
                    temp = india_default[i];
                    india_default[i] = india_default[i+1];
                    india_default[i+1] = temp;
                }
            }
        }
    }
    public static void showTeam(String name)
    {
        System.out.println("This is your Playing XI :-");
        if (name.equals("India"))
        {
            for (int i = 0; i < india_default.length; i++)
                System.out.println(i+1 + ". "  + india_default[i]);
        }
        else if (name.equals("Australia"))
        {
            for (int i = 0; i < australia_default.length; i++)
                System.out.println(i+1 + ". "  + australia_default[i]);
        }
        else if (name.equals("England"))
        {
            for (int i = 0; i < england_default.length; i++)
                System.out.println(i+1 + ". "  + england_default[i]);
        }
        else if (name.equals("New Zealand"))
        {
            for (int i = 0; i < newZealand_default.length; i++)
                System.out.println(i+1 + ". "  + newZealand_default[i]);
        }
        else if (name.equals("Pakistan"))
        {
            for (int i = 0; i < pakistan_default.length; i++)
                System.out.println(i+1 + ". "  + pakistan_default[i]);
        }
        System.out.println();
    }

    public static void selectTeam()
    {
        Scanner scan = new Scanner(System.in);
        System.out.println("Choose your team by entering the serial number :-");
        for (int i = 0; i < player_team.length; i++)
            System.out.println(i+1 + ". " + player_team[i]);
        int team_code = scan.nextInt();
        if (team_code > 0 && team_code <= player_team.length)
        {
            int confirm_flag = -1;
            System.out.println("Your choice is team " + player_team[team_code - 1] + ". Are you sure that you wish to continue with this team? Enter Y to confirm or N to change your choice.");
            while (confirm_flag == -1)
            {
                char confirm = scan.next().charAt(0);
                if (confirm == 'Y' || confirm == 'y')
                {
                    confirm_flag = 1;
                    user_team = player_team[team_code-1];
                }
                else if (confirm == 'N' || confirm == 'n')
                {
                    confirm_flag = 0;
                    selectTeam();
                }
                else
                    System.out.println("Please enter a valid choice (Y or N)");
            }
        }
        else
            System.out.println("Invalid choice. Please reload the game and pick a valid team code");
    }

    public static void selectOpponent()
    {
        Scanner scan = new Scanner(System.in);
        for (int i = 0; i < opponent_team.length; i++)
            if (opponent_team[i] == user_team)
                opponent_team[i] = "XXX";
        String temp = "";
        for (int i = 0; i < opponent_team.length - 1; i++)
        {
            if (opponent_team[i].equals("XXX"))
            {
                temp = opponent_team[i];
                opponent_team[i] = opponent_team[i+1];
                opponent_team[i+1] = temp;
            }
        }
        System.out.println("Choose your opponent team by entering the serial number :-");
        for (int i = 0; i < opponent_team.length - 1; i++)
            System.out.println(i+1 + ". " + opponent_team[i]);
        int op_code = scan.nextInt();
        if (op_code > 0 && op_code < opponent_team.length)
        {
            int confirm_flag = -1;
            System.out.println("Your choice for opponent is team " + opponent_team[op_code - 1] + ". Are you sure that you wish to continue with this team?" +
                    " Enter Y to confirm or N to change your choice.");
            while (confirm_flag == -1)
            {
                char confirm = scan.next().charAt(0);
                if (confirm == 'Y' || confirm == 'y')
                {
                    confirm_flag = 1;
                    op_team = opponent_team[op_code-1];
                }
                else if (confirm == 'N' || confirm == 'n')
                {
                    confirm_flag = 0;
                    selectOpponent();
                }
                else
                    System.out.println("Please enter a valid choice (Y or N)");
            }
        }
        else
        {
            System.out.println("PLEASE ENTER A VALID CODE!");
            selectOpponent();
        }
    }

    public static void teamManagement(String user_team)
    {
        Scanner scan = new Scanner(System.in);
        int confirm_flag = -1;
        while (confirm_flag == -1)
        {
            char team_management = scan.next().charAt(0);
            if (team_management == 'Y' || team_management == 'y')
                confirm_flag = 1;
            else if (team_management == 'N' || team_management == 'n')
                break;
            else
                System.out.println("Please enter a valid choice (Y or N)");  // ERROR! If user enters more than one character
        }
        if(confirm_flag == 1)
        {
            showTeam(user_team);
            String temp = "";
            System.out.println("Select your playing XI by typing the player code. You must select balanced number of batsmen and bowlers to have a decent target to chase!");
            int swap_flag = 1;
            while (swap_flag == 1)
            {
                int t = 0;
                while (t <= 10)
                {
                    int select = scan.nextInt();
                    if (select >= 1 && select <= 16)
                    {
                        if (user_team.equals("India"))
                        {
                            selected_team[t] = india_default[select - 1];
                            india_default[select - 1] = "XXX";
                        }
                        else if (user_team.equals("Australia"))
                        {
                            selected_team[t] = australia_default[select - 1];
                            australia_default[select - 1] = "XXX";
                        }
                        else if (user_team.equals("England"))
                        {
                            selected_team[t] = england_default[select - 1];
                            england_default[select - 1] = "XXX";
                        }
                        else if (user_team.equals("New Zealand"))
                        {
                            selected_team[t] = newZealand_default[select - 1];
                            newZealand_default[select - 1] = "XXX";
                        }
                        else if (user_team.equals("Pakistan"))
                        {
                            selected_team[t] = pakistan_default[select - 1];
                            pakistan_default[select - 1] = "XXX";
                        }
                        t++;
                    }
                    else
                        System.out.println("Please enter a valid player code");
                }
                swap_flag = 0;
            }
        }
       /* else
        {
            DEFAULT PLAYING XI OF EACH TEAM !!!!!!!!!!!!!!!!!
        }  */
    }

    public static void main(String[] args)
    {
        selectTeam();
        System.out.println("You have chosen to continue with team " + user_team + ". " +
                "If you want to go for team management, type 'Y' or go with the default Playing XI by typing 'N'.");
        teamManagement(user_team);
        selectOpponent();
        System.out.println("You have chosen to continue with team " + op_team + " as your opponent.");
        String playingXI[] = new String[11];
        playingXI = getPlayingXI(user_team);
    }
}