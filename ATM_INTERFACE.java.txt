import java.io.*;
import java.util.*;
import java.time.format.DateTimeFormatter;
import java.time.LocalDateTime;
public class ATM_INTERFACE{
    String Full_Name,Dob,Gender;
    String Gender1="M";
    String Gender2="m";
    String Gender3="F";
    String Gender4="f";
    String User_name,Account_Number,Password,Pin,Phone;
    String Transaction_his="Your Transaction History:\n";
    Scanner s=new Scanner(System.in);
    DateTimeFormatter dtf = DateTimeFormatter.ofPattern("dd-MM-yyyy HH:mm:ss");
    LocalDateTime now=LocalDateTime.now();
    float Balance=0f;
    int Transactions=0;

    public void View_profile(){
        System.out.println("Your Profile:\n");
        System.out.println("Full-Name:  "+this.Full_Name);
        System.out.println("Date of Birth:  "+this.Dob);
        System.out.println("Gender:  "+this.Gender);
        System.out.println("Username:  "+this.User_name);
        System.out.println("Password:  "+this.Password);
        System.out.println("Account Number:  "+this.Account_Number);
        System.out.println("4-Digith-pin:  "+this.Pin);
        System.out.println("Phone:  "+this.Phone); 
    }
    public void Register(){
        System.out.println("....Registration....\n");
        System.out.println("\nEnter Full Name: ");
        this.Full_Name=s.nextLine();
        System.out.println("Enter Date of Birth(dd/mm/yyyy): ");
        this.Dob=s.nextLine();
        System.out.println("Enter Gender(M/F):  ");
        this.Gender=s.nextLine();
        while(!(((this.Gender).equals(this.Gender1) || (this.Gender).equals(this.Gender2)  ||  (this.Gender).equals(this.Gender3)  ||  (this.Gender).equals(this.Gender4)))){
            System.out.println("Invalid...Please enter correct Gender(M/F):  ");
            this.Gender=s.nextLine();
        }
        if(this.Gender.equals(this.Gender1)  ||  this.Gender.equals(this.Gender2)){
            this.Gender="Male";
        }
        else{
            this.Gender="Female";
        }
        System.out.println("Enter Username:  ");
        this.User_name=s.nextLine();
        System.out.println("Enter Password:  ");
        this.Password=s.nextLine();
        System.out.println("Enter Account Number:   ");
        this.Account_Number=s.nextLine();
        while((Account_Number.length())!=10){
            System.out.println("!!! Please Enter Valid 10 digit Account Number: ");
            this.Account_Number=s.nextLine();
        }
        System.out.println("Enter 4-Digit-Pin:  ");
        this.Pin=s.nextLine();
        while((Pin.length())!=4){
            System.out.println("!!! Please Enter Valid 4 Digit Pin:  ");
            this.Pin=s.nextLine();
        }
        System.out.println("Enter Your Phone Number:  ");
        this.Phone=s.nextLine();
        while((Phone.length())!=10){
            System.out.println("!!! Please Enter Valid 10 digit Mobile Number");
            this.Phone=s.nextLine();
        }
        System.out.println("\n-----You are Successfully Registered...-----\n");
        System.out.println("Kindly Login to your account to perform any trainsactions...");
    }
    public boolean Login(){
        boolean log=false;
        while(!log){
            String Acc_num,pin;
            System.out.println("Enter Account Number:  ");
            Acc_num=s.nextLine();
            if(Acc_num.equals(Account_Number)){
                System.out.println("Enter 4 digit Pin:  ");
                pin=s.nextLine();
                while(!log){
                    if(pin.equals(Pin)){
                        System.out.println("Logged in Successfully...");
                        log=true;
                    }
                    else{
                        System.out.println("Enter Correct Pin!!");
                        break;
                    }
                }
            }
            else{
                System.out.println("Register to login...");
            }
        }
        return log;
    }
    public void Deposit(){
        System.out.println("Enter the Amount to deposit into your Account:  ");
        float Deposit_amt;
        Deposit_amt=s.nextFloat();
        if(Deposit_amt>500000f){
            System.out.println("This ATM is not capable to deposit money beyond 5,00,000/-");
        }
        else{
            Balance=Balance+Deposit_amt;
            Transactions+=1;
            System.out.println("Successfully deposited Rs. "+Deposit_amt+" into your account at "+dtf.format(now));
            System.out.println("Your Current Balance after this transaction is:  "+Balance);
            String History=" ";
            History="\n Rs "+Deposit_amt+" Deposited at"+dtf.format(now)+" .\n";
            Transaction_his=Transaction_his.concat(History);
        }
    }
    public void Withdraw(){
        System.out.println("Enter the amount you want to withdraw:  ");
        float Withdraw_amt;
        Withdraw_amt=s.nextFloat();
        if(Withdraw_amt<500000){
            if(Withdraw_amt>Balance){
                System.out.println("Sorry!..Insufficient Balance...");
            }
            else{
                Balance=Balance-Withdraw_amt;
                Transactions=Transactions+1;
                System.out.println("Successfully withdraw Rs. "+Withdraw_amt+" from your account at "+dtf.format(now));
                System.out.println("Your current Balance after transaction is: "+Balance);
                String History=" ";
                History="\n Rs "+Withdraw_amt+" Withdrawn at"+dtf.format(now)+" .\n";
                Transaction_his=Transaction_his.concat(History);
            }
        }
        else{
            System.out.println("This ATM cannot dispence Money more than 500,000/-");
        }
    }
    public void Transfer(){
        System.out.print("Enter the User Name to transfer to:  \n");
        String Transfer_name;
        Transfer_name=s.nextLine();
        System.out.println("Enter the amount to transfer to : ");
        float Total_amt;
        Total_amt=s.nextFloat();
        if(Total_amt<500000){
            if(Total_amt>Balance){
                System.out.println("Sorry! Amount cannot be transfered due to Insufficient Balance.");
                System.out.println("Your Balance was: "+Balance);
            }
            else{
                Balance=Balance-Total_amt;
                Transactions=Transactions+1;
                System.out.println("Successfully Transfered Rs. "+Total_amt+"to "+Transfer_name+" from your account at "+dtf.format(now));
                System.out.println("Your current Balance after this transaction is: "+Balance);
                String History=" ";
                History="\n Rs "+Total_amt+" was transfered to "+Transfer_name+"'s account from your account at "+dtf.format(now)+" .\n";
                Transaction_his=Transaction_his.concat(History);
            }
        }
        else{
            System.out.println("Cannot transfer money beyond 5,00,000/-");
        }
    }
    public void Transcation_history(){
        if(Transactions==0){
            System.out.println("No Transactions");
        }
        else{
            System.out.println(Transaction_his);
        }
    }
    public void Check_Bal(){
        System.out.println("\n Balance amount is: "+Balance);
    }
    public static void main(String args[]){
        Scanner input = new Scanner(System.in);
        System.out.println("\n-----  Welcome to ATM  -----\n");
        System.out.println("\n1.REGISTER (New user should register first)\n 2. EXIT ");
        System.out.println("Your choice: ");
        int choice;
        choice=input.nextInt();
        if(choice==1){
            ATM_INTERFACE atm=new ATM_INTERFACE();
            atm.Register();
            while(choice==1){
                System.out.println("\n Select any one option: ");
                System.out.println("1.Login (if already Registered)\n2.Exit");
                System.out.println("Your option: ");
                int opt;
                opt=input.nextInt();
                if(opt==1){
                    if(atm.Login()){
                        while(true){
                            System.out.println("\n\n This ATM is able to perform these operations: \n ");
                        System.out.println("1.View Profile\n 2.Deposit\n 3.Withdraw\n 4.Transfer\n 5.Transaction history\n 6.Check Balance\n 7.Exit");
                        System.out.println("Enter your option: ");
                        int select;
                        select=input.nextInt();
                        switch(select){
                            case 1 : atm.View_profile();
                            break;
                            case 2 : atm.Deposit();
                            break;
                            case 3 : atm.Withdraw();
                            break;
                            case 4 : atm.Transfer();
                            break;
                            case 5 : atm.Transcation_history();
                            break;
                            case 6 :atm.Check_Bal();
                            break;
                            case 7 : System.out.println("\nThank you\n...Visit Again...:)");
                                    System.exit(0);
                            break;
                            default:System.out.println("Invalid option!...Enter Valid option...");
                        }
                    }
                }
            }
            else{
                System.out.println("\n Thank you...Visit Again...:)");
                System.exit(0);
            }
        }
    }
    else{
        System.out.println("\n Thank you...Visit Again...:)");
        System.exit(0);
    }      
    
}
}