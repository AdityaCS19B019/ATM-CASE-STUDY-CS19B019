# ATM-CASE-STUDY-CS19B019
IN THIS CODE,FILE OF OUTPUT AND FILE OF FLOW CHART HAS BEEN UPLOADED/U CAN CONTACT cs19b019@iittp.ac.in
INSTRUCTIONS TO USE CODE
FIRST ALL ACCOUNT NUMBERS AND PASSWORDS ARE GIVEN IN ARRAY IN CUSTOMER CLASS
ADMIN ID IS 19019 AND ADMIN PASSWORD IS 99999,USE WHENEVER REQUIRED
FROM THE BELOW THE ACUAL CODE IS WRITTEN
package com.company;

import java.util.Scanner;
class Customer
{
    int p,flag,a,check,wtdrw,counttmsofwdrw=0,depo,countofdep=0;
    private int acc[]={12345,12346,12347,12348,12349,12350,12351,12352,12353,12354};
    //the above assigns the account numbers
    private int pin[]={98760,98759,98758,98757,98756,98755,98754,98753,98752,98751};
    //the above assigns the passwors for corresponding account numbers
    private int bal[]={50000,56000,85450,65400,98700,120500,359000,45000,58900,25000};
    //this is the initial balance of corresponding account numbers
    private int noofdep[]={0,0,0,0,0,0,0,0,0,0};
    private int noofwdrw[]={0,0,0,0,0,0,0,0,0,0};
    public int checkacc(int a)
    {
        this.a=a;
        for(int j=0;j<10;j++)
        {
            if(acc[j]==a)
            {     flag=1;
                  check=j;
                  break;
            }
            else
                flag=0;
        }
        return flag;
    }
    public int checkpin(int p)
    {
        this.p=p;
        if(p==pin[check])
            return 1;
        else
            return 0;

    }
    public void withdraw(int wtdrw)
    {
        this.wtdrw=wtdrw;
        if(bal[check]>=wtdrw)
        {
            bal[check] = bal[check] - wtdrw;
            System.out.println("*** money withdrawed successfully ***");
            noofwdrw[check]++;
            counttmsofwdrw++;
        }
        else
            System.out.println("*** money in your account is not sufficient to withdraw ***");
    }
    public void minstatement()
    {
        System.out.println("**** you had withdrawed"+ noofwdrw[check]+ " no of times ****");
        System.out.println("**** you had deposited money "+ noofdep[check]+ " times ****");
        System.out.println("**** your final balance is "+bal[check]+" ****");
    }
    public void balenqry()
    {
        System.out.println("**** after all transactions your balance is"+ bal[check]+" ****");
    }
    public void deposit(int depo)
    {
        this.depo=depo;
        bal[check]=bal[check]+depo;
        System.out.println("**** you have deposited Rs"+ depo+"successfully ****");
        noofdep[check]++;
        countofdep++;
    }
    public void nooftra()
    {
        System.out.println("*** total no of deposits up to now are "+countofdep+" ***");
        System.out.println("*** total no of withdraws up to now are "+counttmsofwdrw+" ***");
    }
    public void reset()
    {
        counttmsofwdrw=0;
        countofdep=0;
        System.out.println("*** all transactions are resetted now ***");
    }

}
class Admin
{
    private int atmbal=1000000;
    int amwdrw,atmdep;
    public int issufftowdrw(int amwdrw)
    {
        this.amwdrw=amwdrw;
        if(amwdrw<=atmbal)
        {
            atmbal=atmbal-amwdrw;
            return 1;
        }
        else
            return 0;
    }
    public void depinatm(int atmdep)
    {
        this.atmdep=atmdep;
        atmbal=atmbal+atmdep;
    }
    public void showatmbal()
    {
        System.out.println("*** the ramaining balance in atm right now is "+atmbal+" ***");
    }


}
public class Main {

    public static void main(String[] args)
    {
        Scanner scan=new Scanner(System.in);
        Customer c=new Customer();
        Admin a=new Admin();
	     int i=1;
	     while(i>0)
         {
             System.out.println("-------------------------------------------------------------------------------");
             System.out.println("    welcome");
             System.out.println("    press 1 if u are a customer");
             System.out.println("    press 2 if u are admin");
             int re=scan.nextInt();
               if(re==1)
               {
                       System.out.println("    enter your account number");
                       int acc1 = scan.nextInt();
                       if (c.checkacc(acc1) == 1) {
                           System.out.println("     enter your pin");
                           int pin1 = scan.nextInt();
                           if (c.checkpin(pin1) == 1) {

                               System.out.println("    press 1 to select withdraw");
                               System.out.println("    press 2 to select ministatement");
                               System.out.println("    press 3 to select balance enquiry");
                               System.out.println("     press 4 to deposit money");
                               int re1 = scan.nextInt();
                               if (re1 == 1) {
                                   System.out.println("    enter the amount u want to withdraw");
                                   int wtd = scan.nextInt();
                                   if (a.issufftowdrw(wtd) == 1) {
                                       c.withdraw(wtd);
                                   } else
                                       System.out.println("*** money is not sufficient in atm ***");
                               }
                               if (re1 == 2) {
                                   c.minstatement();
                               }
                               if (re1 == 3) {
                                   c.balenqry();
                               }
                               if (re1 == 4) {
                                   System.out.println("enter the amount you want to deposit");
                                   int dep = scan.nextInt();
                                   c.deposit(dep);
                                   a.depinatm(dep);
                               }

                           } else {
                               System.out.println("your entered pin is wrong please check again");
                           }
                       } else {
                           System.out.println("sorry your credentials are not found plese check again");
                       }


               }
               if(re==2)
               {
                   System.out.println("enter your admin id");
                   if(scan.nextInt()==19019)
                   {
                       System.out.println("enter your password");
                       if(scan.nextInt()==99999)
                       {
                           System.out.println("press 1 to check atm balance");
                           System.out.println("press 2 to check no of transactions done today");
                           System.out.println("press 3 to reset all transactions");
                           System.out.println("press 4 to deposit in atm");
                           int k=scan.nextInt();
                           if(k==1)
                           {a.showatmbal();}
                           if(k==2)
                           {c.nooftra();}
                           if(k==3)
                           {c.reset();}
                           if(k==4)
                           {
                               System.out.println("    enter the money deposited");
                               int depos=scan.nextInt();
                               a.depinatm(depos);

                           }
                       }
                       else
                           System.out.println("****wrong password\n****this incident will bw reported");
                   }
                   else
                       System.out.println("****  sorry wrong id \n*****this incident will be reported");
               }

         }
    }
}
