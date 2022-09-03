#Account
Funçoes de conta em Java.

package application;

import java.util.Locale;
import java.util.Scanner;

import entities.Account;

public class Program {

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		Locale.setDefault(Locale.US);
		Account account;
		
		System.out.print("Enter account number: ");
		int number = sc.nextInt();
		System.out.print("Enter account holder: ");
		sc.nextLine();
		String holder = sc.nextLine();
		System.out.print("Is there an initial deposit(y/n)?: ");
		char response = sc.next().charAt(0);
		if(response == 'y') {
			System.out.println("Enter initial deposit value");
			double initialDeposit = sc.nextDouble();
			account = new Account(number, holder, initialDeposit);
		}else {
			account = new Account(number, holder);
		}
		
		System.out.println();
		System.out.println("Account data: ");
		System.out.println(account);
		
		System.out.println();
		System.out.print("Enter a deposit value: ");
		double depositValue = sc.nextDouble();
		account.deposit(depositValue);
		System.out.println("updated account data: ");
		System.out.println(account);
		
		System.out.println();
		System.out.print("Enter a withdraw value: ");
		double withdrawValue = sc.nextDouble();
		
		if( withdrawValue > Account.getBalance()) {
			System.out.println("INSUFICIENT BALANCE");
		}else {
			account.withdraw(withdrawValue);
			System.out.println("updated account data: ");
			System.out.println(account);
		}
		
		
		
		sc.close();
	}

}

package entities;

public class Account {

	private int number;
	private String holder;
	private static double balance;
	
	
	public Account(int number, String holder) {
		super();
		this.number = number;
		this.holder = holder;
	}


	public Account(int number, String holder, double initialDeposit) {
		this.number = number;
		this.holder = holder;
		deposit(initialDeposit);
	}


	public int getNumber() {
		return number;
	}

	public String getHolder() {
		return holder;
	}


	public void setHolder(String holder) {
		this.holder = holder;
	}


	public static double getBalance() {
		return balance;
	}

	public void deposit(double amount) {
		balance += amount;
	}
	public void withdraw(double amount) {
		balance -= amount + 5.0;
	}
	
	public String toString() {
		return 	"Account "
				+ number
				+ ", Holder: "
				+ holder
				+ ", Balance: $ "
				+ String.format("%.2f", balance);
	}


	
}
