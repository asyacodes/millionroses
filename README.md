# millionroses
there is a file that stores information about the shop with flowers. file contains names of deliver boys and type of payments during the determined month. 

/*
 ============================================================================
 Name        : Yespanova.Assyl.c
 Author      : Assyl Yespanova
 Description : "Million Roses". Assignment 1. CSCI 151.
 ============================================================================
 */
#include <stdio.h>
#include <string.h>

/*we are storing the data in an array of struct */

typedef struct {
	int sale_id, date, quantity;
	char type[201];
	double total_cost;
	char arrangement [201];
	char payment[201];
	int delivery;
	char courier[201];

} database;


int main ()
{
	setvbuf (stdout, NULL, _IONBF, 0);

	/*opening the file and scanning the data from it*/

	FILE *infile;
	infile = fopen("flower_sales.txt", "r");

	database database[201];

	int i = 0;
	do {
		i++;

		fscanf(infile, "%i %i %i %s %lf %s %s %i %s\n", &database[i].sale_id, &database[i].date, &database[i].quantity, database[i].type, &database[i].total_cost, database[i].arrangement, database[i].payment, &database[i].delivery, database[i].courier);

	} while(!feof(infile));

		int size = i;
		int day;

	/*now the user should enter a number for the day*/

	while(1)
	{
		printf ("Please, input the day in the form of an integer (1-31).\n");
		scanf ("%i", &day);

	/*in case if the user have entered inappropriate number*/

	if (day < 1 || day > 31)
	{
		printf ("The day you've entered is incorrect");
		break;
	}
	else

	/*in case if the number is correct, the programme runs*/

	{

		/*declare all necessary variables*/

		int i, j;
		int orders = 0;
		int individual_flowers = 0;
		int small_bouquet = 0;
		int box_of_flowers = 0;
		int big_bouquet = 0;
		int gift = 0;
		char type_of_gift[201][201];
		double cost_in_total = 0;
		double Cash = 0;
		double Epay_Kazkom = 0;
		double halyq_bank = 0;
		double web_money = 0;
		double PayPal = 0;
		double qiwi = 0;
		double yandex_money = 0;
		int delivery = 0;
		int deliveries_in_total = 0;
		int pickup = 0;
		int courier_shapaghat = 0;
		int courier_qanat_agha = 0;
		int courier_azat = 0;

		/*running the program*/

		for(i = 1; i <= size; i++) {
			if (database[i].date == day)
			{
				/*calculating the total number of the orders placed for this day*/

				orders++;

				/*adding up all the quantities of purchased individual flowers*/

				individual_flowers = individual_flowers + database[i].quantity;

				cost_in_total = cost_in_total + database[i].total_cost;

				/*by the function "strcmp" each variable is compared with the corresponding string in the file*/

				if (strcmp(database[i].type, "small_bouquet") == 0)
					{small_bouquet++;};

				if (strcmp(database[i].type, "box_of_flowers") == 0)
					{box_of_flowers++;};

				if (strcmp(database[i].type, "big_bouquet") == 0)
					{big_bouquet++;};

				if (strcmp(database[i].type, "gift") == 0)
					{
						for (j = 0; j < 201; j++)

						/*defining the gift into an array*/

					{
						type_of_gift[gift][j] = database[i].arrangement[j];
					}
						gift++;
					}

				/*computing the cost for each type of the payment again by using the "strcmp"*/

				if (strcmp(database[i].payment, "cash") == 0)
					{Cash += database[i].total_cost;}

				if (strcmp(database[i].payment, "Epay_Kazkom") == 0)
					{Epay_Kazkom += database[i].total_cost;}

				if (strcmp(database[i].payment, "halyq_bank") == 0)
					{halyq_bank += database[i].total_cost;}

				if (strcmp(database[i].payment, "web_money") == 0)
					{web_money += database[i].total_cost;}

				if (strcmp(database[i].payment, "PayPal") == 0)
					{PayPal += database[i].total_cost;}

				if (strcmp(database[i].payment, "qiwi") == 0)
					{qiwi += database[i].total_cost;}

				if (strcmp(database[i].payment, "yandex_money") == 0)
					{yandex_money += database[i].total_cost;}

				/*defining how many deliveries were made and the total cost of deliveries for the given day*/

				if (database[i].delivery != 0)
				{
					delivery += database[i].delivery;
					deliveries_in_total++;
				}

				if (strcmp(database[i].courier, "pickup") == 0)
					{pickup += database[i].delivery;}

				if (strcmp(database[i].courier, "shapaghat") == 0)
					{courier_shapaghat++;}

				if (strcmp(database[i].courier, "qanat_agha") == 0)
					{courier_qanat_agha++;}

				if (strcmp(database[i].courier, "azat") == 0)
					{courier_azat++;}
			}
		}

		/*now the quantity of the each type of the order is going to be printed out*/

		printf ("Orders made at that day:%i\n", orders);
		printf ("Individual flowers were purchased:%i \n", individual_flowers);
		printf ("Small bouquets were purchased:%i \n", small_bouquet);
		printf ("Big bouquets were purchased:%i \n", big_bouquet);
		printf ("Gifts were purchased:%i \n", gift);

		/*printing how many gifts were purchased that day and listing them by the types*/

		if(gift != 0)
		{
			int k;
			for(k = 0; k < gift; k++)
				printf("database(s): %s\n ",  type_of_gift[k]);
			printf("\n");
		}

		/*at this stage all required outputs for payment are going to be printed out*/

		printf("The total cost of the orders for the given day is %.3lf\n\n", cost_in_total);
		printf("1. Cash: %.3lf\n", Cash);
		printf("2. Epay_Kazcom: %.3lf\n", Epay_Kazkom);
		printf("3. halyq_bank: %.3lf\n", halyq_bank);
		printf("4. web_money: %.3lf\n", web_money);
		printf("5. PayPal: %.3lf\n", PayPal);
		printf("6. qiwi: %.3lf\n", qiwi);
		printf("7. yandex_money: %.3lf\n\n", yandex_money);
		printf("Deliveries were made:%i\n", deliveries_in_total);
		printf("Total cost of deliveries for the day is %i\n\n", delivery);

		if(deliveries_in_total > 0)

		/*we need to define who made the number of maximum deliveries for this day and it will be printed*/

		{
			if ((courier_shapaghat >= courier_qanat_agha) && (courier_shapaghat >= courier_azat))
				printf ("The maximum deliveries was made by courier Shapagat and it is equal to %i\n", courier_shapaghat);

			else if ((courier_qanat_agha >= courier_shapaghat) && (courier_qanat_agha >= courier_azat))
				printf ("The maximum deliveries was made by courier Qanat agha and it is equal to %i\n", courier_qanat_agha);

			else if ((courier_azat >= courier_shapaghat) && (courier_azat >= courier_qanat_agha ))
				printf ("The maximum deliveries was made by courier Azat and it is equal to %i\n", courier_azat);
		}
			else
			printf("There were no deliveries at this day!\n");

		}
	}

		/*closing the file*/

		fclose(infile);

		return 0;


}
