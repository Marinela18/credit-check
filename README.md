# credit-check
Unit 16 Procedural Programming Credit Card Check application
#include<stdio.h>
#include<conio.h>

int c[20], l;

void main()
{
	long long int a;

	printf("Please enter the long number on your card ");
	scanf_s("%lld", &a);
	digits(a);
}

int digits(long long int b)
{
	int i=0;
	long long int a;
	a = b;
	while (a >= 10)
	{
		a = a / 10;
		i++;
	}
	c[i + 1] = '\0';
	l = i + 1;
	while (i >= 0)
	{
		c[i] = b % 10;
		b = b / 10;
		i--;
	}
	if (l == 15 || l == 16)
	{
		printf("The card number introduced is valid \n");
		luhn();
	}
	else
		printf("The card number introduced is not valid \n");
	return 0;
}

int luhn()
{
	int s, se=0, so=0, b[20], d;

	for (int i = l - 1, j = 0; i >= 0; i--, j++)
		b[j] = c[i];

	for (int i = 0; i < l; i++)
		if (i % 2 == 0)
			so = so + b[i];
		else
		{
			d = b[i] * 2;
			if (d >= 10)
				d = d / 10 + d % 10;
			se = se + d;
		}

	s = se + so;

	if (s % 10 == 0)
	{
		printf("The card number has passed Luhn's test \n");
		type();
	}
	else
		printf("The card number did not pass Luhn's test \n");
	return 0;
}

int type()
{
	int i=0;

	if (c[i] == 4)
		printf("Card type identified: VISA \n");
	else if (c[i] == 3 && (c[i + 1] == 4 || c[i + 1] == 7))
		printf("Card type identified: American Express \n");
	else if (c[i] == 5 && (c[i + 1] == 0 || c[i + 1] == 5))
		printf("Card type identified: MasterCard \n");
	else if (c[i] == 6)
	{
		if (c[i + 1] == 5)
			printf("Card type identified: Discover \n");
		if ((c[i + 1] && c[i + 2]) == 4)
			printf("Card type identified: Discover \n");
		if (c[i + 1] == 0 && c[i + 2] == 1 && c[i + 3] == 1)
			printf("Card type identified: Discover \n");
		else
			printf("Card type couldn't be identified \n");
	}
	else
		printf("Card type couldn't be identified \n");
	return 0;
}
