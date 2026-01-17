# alapaca-hotel
//ALPACA HOTEL SYSTEM
//SCS3/2593/2025
//SCS3/150749/2025
//SCS3/150728/2025
//SCS3/150108/2025
#include<stdio.h>
#include<stdlib.h>

typedef struct{
char roomtype[15];
int occupants;
int nights;
}Room;

typedef struct{
char name[50];
int phoneNo;
char email[50];
int bill;
Room room[10];
}Details;

Details details[50];
int i=0;
int j;

void bookRoom()
{
    printf("enter customer name:");
    scanf("%s",details[i].name);
    printf("enter phone number:");
    scanf("%d", &details[i].phoneNo);
    printf("enter email:");
    scanf("%s",details[i].email);
    printf("enter number of rooms:");
    scanf("%d", &j);
    int total=0;

    for(int k=0;k<j;k++){
        int choice;
        printf("enter room type:\n1.premium @30000 per person\n2.Beach view @25000 per person\n3.Normal @20000 per person\n Choice:");
        scanf("%d", &choice);
        printf(" number of people\n");
        scanf("%d", &details[i].room[k].occupants);
        printf("enter number of nights \n");
        scanf("%d", &details[i].room[k].nights);
        int p;

        if(choice==1){
           p=30000*details[i].room[k].occupants*details[i].room[k].nights;
           total+=p;
           sprintf(details[i].room[k].roomtype,"Premium");
        }else if(choice==2){
           p=25000*details[i].room[k].occupants*details[i].room[k].nights;
           total+=p;
           sprintf(details[i].room[k].roomtype,"Beach View");
        }else if(choice==3){
           p=20000*details[i].room[k].occupants*details[i].room[k].nights;
           total+=p;
           sprintf(details[i].room[k].roomtype,"Normal");
        }
    }

    details[i].bill=total;

    char name[100];
    sprintf(name,"%s.txt",details[i].name);
    FILE*fc=fopen(name,"w");
     if(fc==NULL){
        printf("Details could not be saved");
    }
    fprintf(fc,"Customer details\n");
    fprintf(fc,"Name:\t%s\n",details[i].name);
    fprintf(fc,"Phone number:\t%d\n",details[i].phoneNo);
    fprintf(fc,"Email:\t%s\n",details[i].email);
    fprintf(fc,"Rooms Booked:\t%d\n",j);
    fclose(fc);
    printf("Details saved successfully\n");

    sprintf(name,"%s_bill.txt",details[i].name);
    FILE*fb=fopen(name,"w");
     if(fb==NULL){
        printf("Bill could not be saved");
    }
    fprintf(fb,"Bill\n---------------------\n");
    for(int k=0;k<j;k++){
    fprintf(fb,"Room %d:%s\n",k+1,details[i].room[k].roomtype);
    fprintf(fb,"Occupants:%d\n",details[i].room[k].occupants);
    fprintf(fb,"Nights:%d\n",details[i].room[k].nights);
    }
    fprintf(fb,"Total bill=%d",details[i].bill);
    fclose(fb);
    printf("Bill Generated\n");
    i++;
}

void viewBooking()
{
    char name[100];
    char line[256];
    char filename[100];

    printf("Enter Customer's name: ");
    scanf("%s",name);

    sprintf(filename,"%s.txt",name);

    FILE *fp;
    fp = fopen(filename,"r");
    if(!fp)
    {
        printf("No record found for %s\n\n", name);
        return;
    }

    printf("This is the Customer's Details:\n");

    while(fgets(line, sizeof(line), fp))
    {
        printf("%s", line);
    }
    fclose(fp);
}

void viewBill()
{
    char name[100];
    char line[256];
    char filename[100];

    printf("Enter Customer's name: ");
    scanf("%s",name);

    sprintf(filename,"%s_bill.txt",name);

    FILE *fp;
    fp = fopen(filename,"r");
    if(!fp)
    {
        printf("No record found for %s\n\n", name);
        return;
    }

    printf("This is the Customer's Bill:\n");

    while(fgets(line, sizeof(line), fp))
    {
        printf("%s", line);
    }
    fclose(fp);
}

int main()
{
    int choice;
    do{
        printf("\nWELCOME TO ALPACA HOTEL\n");
        printf("1.Book room\n");
        printf("2.View customers details\n");
        printf("3.View Bill\n");
        printf("4.Exit\n");
        printf("Enter choice: ");
        scanf("%d",&choice);

        switch(choice)
        {
        case 1:
            bookRoom();
            break;
        case 2:
            viewBooking();
            break;
        case 3:
            viewBill();
            break;
        case 4:
            printf("Exiting...\n");
            break;
        default:
            printf("Invalid choice\n");
        }
    }while(choice!=4);

    return 0;
}
