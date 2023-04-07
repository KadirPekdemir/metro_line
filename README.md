# metro_line
This code finds the shortest path on the metro line.
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <Math.h>
#define SIZE 10


 typedef struct MetroStation {
     char name[20];
     double x;
     double y;

 }MetroStation;


 typedef struct MetroLine {
     char color[20];
     MetroStation MetroStations[SIZE];

 }MetroLine;


 typedef struct MetroSystem {
     char name[20];
     MetroLine MetroLines[SIZE];

 }MetroSystem;


 int equals(MetroStation s1, MetroStation s2){
     if(strcmp(s1.name,s2.name))
        return 1;
     else
        return 0;
 }






//this method adds stations to the MetroLines array.
 void addStation(MetroLine *a,MetroStation b){
     for(int i=0;i<SIZE;i++){
        if(a->MetroStations[i].name[0]=='\0'){
            a->MetroStations[i]=b;
            break;
        }
     }
 }


 //This method checks the status of the given station on the line.
 int hasStation(MetroLine a,MetroStation b){
     int size=arraySize2(a);
        for ( int i = 0; i<size; i++) {
            if(a.MetroStations[i].x == b.x){

                return 1;
            }


        }
        return 0;
 }







//this method returns the first station on the line.
 MetroStation getFirstStop(MetroLine a){
     MetroStation empty;
     if(a.MetroStations[0].name[0]=='\0'){
        return empty;
     }
     else
        return a.MetroStations[0];



 }





//this method returns the next station from the entered station on the given line
 MetroStation getNextStop(MetroLine a, MetroStation b){
     int size=arraySize2(a);
     MetroStation empty =  a.MetroStations[9];
        for ( int i = 0; i<size-1; i++) {
            if(a.MetroStations[i].x == b.x){

                return a.MetroStations[i+1];
            }
        }

        return empty;
    }






//this method returns the station before the entered station on the given line
 MetroStation getPreviousStop(MetroLine a,MetroStation b){
     MetroStation empty =  a.MetroStations[9];
     int size=arraySize2(a);
      for ( int i = 1; i<size; i++) {
            if(a.MetroStations[i].x == b.x){

                return a.MetroStations[i-1];
            }


        }

        return empty;
 }





//this method adds metro lines to MetroSystem array
 void addLine(MetroSystem *a, MetroLine b){
     for(int i=0;i<SIZE;i++){
        if(a->MetroLines[i].color[0]=='\0'){
            a->MetroLines[i]=b;
           break;
        }

     }
 }




//this method prints the entered metro line and stations respectively.
 void printLine(MetroLine a){
     printf("Metroline %s :  ",a.color);
     printf("%s ",a.MetroStations[0].name);
     for(int i=1;i<SIZE;i++){
            if(a.MetroStations[i].name[0]=='\0'){
                printf(".");
                break;
            }

        printf(", %s ",a.MetroStations[i].name);


     }
     printf("\n");

 }




 //this method returns the size of the entered array.
 int arraySize2(MetroLine a){
     int size=0;
        for (int j= 0; j<SIZE; j++) {
            if (a.MetroStations[j].name[0]=='\0') {
                break;
            }
            else
                size++;
        }
        return size;
 }



 //this method returns the size of the entered array.
 int arraySize(MetroStation a[]){
     int size = 0;
     for(int i=0;i<SIZE;i++){
        if(a[i].name[0]=='\0'){
            break;
        }
        else{
            size++;
        }
      }
      return size;

 }



 //this method prints the most convenient way array
  void printPaths(MetroStation a[]){
      int size=arraySize(a);
      for(int j=0;j<size;j++){
        printf("%d. %s\n",j+1,a[j].name);

      }

 }





//this method calculates line distance
 double getDistanceTravelled(MetroStation a[]){
     int size=arraySize(a);
     double sum = 0;
     for(int i=0;i<size-1;i++){
        sum += pow((pow((a[i+1].x-a[i].x),2)+pow((a[i+1].y-a[i].y),2)),0.5);
     }
     return sum;
 }




//this method calculates the distance between two given points
double findDistance(double x, double y, double x_, double y_){
        double distance;
        distance = pow((pow(x-x_, 2)+pow(y-y_, 2)), 0.5);
        return  distance;
    }
 MetroStation findNearestStation(MetroSystem a,double x, double y){
     double minSubstition = 10000;

     for(int i=0;i<SIZE;i++){
        for(int j=0;j<SIZE;j++){
            if(findDistance(x ,y , a.MetroLines[i].MetroStations[j].x,a.MetroLines[i].MetroStations[j].y)<minSubstition){
                minSubstition=findDistance(x ,y , a.MetroLines[i].MetroStations[j].x,a.MetroLines[i].MetroStations[j].y);
            }
        }
     }
     for(int i=0;i<SIZE;i++){
         for(int j=0;j<SIZE;j++){
            if(findDistance(x ,y , a.MetroLines[i].MetroStations[j].x,a.MetroLines[i].MetroStations[j].y)==minSubstition){
                return a.MetroLines[i].MetroStations[j];
            }
         }
     }

 }




 //this method collects the neighboring stations of the station into an array.
  void getNeighboringStations(MetroSystem a,MetroStation b,MetroStation neigboringStations[]){

      for(int i=0;i<SIZE;i++){
        for(int j=0;j<SIZE;j++){
            if(a.MetroLines[i].MetroStations[j].name==b.name){
               for(int k=0;k<SIZE;k++){
                   if(neigboringStations[k].name[0]=='\0'){
                        neigboringStations[k]=a.MetroLines[i].MetroStations[j-1];
                        neigboringStations[k+1]=a.MetroLines[i].MetroStations[j+1];
                   }
               }
            }
        }
      }
   }





//I put it in the comment line because the 13.function doesn't work.
   /* void findPath(MetroStation start,MetroStation finish,MetroStation path[]){
        MetroStation partialPath[SIZE];
        recursiveFindPath(start,finish,partialPath[],path[]);


    }
   void recursiveFindPath(MetroStation start,MetroStation finish,MetroStation partialPath[],MetroStation bestPath[]){
        if(){

        }
        else if(equals(start,finish)){
            bestPath=partialPath;
            return bestPath;
            break;

        }
        else{
            MetroStation neigboringStations[SIZE]=NULL;
            getNeighboringStations(istanbul,start,neigboringStations[]);
            for(int i=0;i<SIZE;i++){
                MetroStation duplicatePath[SIZE]=partialPath[SIZE];
            for(int j=0;j<SIZE;j++){
                if(duplicatePath[j].name[0]=='/0'){
                    duplicatePath[j]=start;
                    break;
                }
            }
            recursiveFindPath(neigboringStations[i],finish,duplicatePath[],currentPath[]);
          }


        }

    }



MetroStation duplicatePath[SIZE]=partialPath[SIZE];
            for(int i=0;i<SIZE;i++){
                if(duplicatePath[i].name[0]=='/0'){
                    duplicatePath[i]=start;
                    break;
                }
            }



*/




MetroSystem istanbul = {"istanbul", '\0'};
int main()
{
	int i;
	double myX=1, myY=2;
	double goalX=62, goalY=45;

	// define 3 metro lines, 9 metro stations, and an empty myPath
	MetroLine red={'\0'}, blue={'\0'}, green={'\0'};
	MetroStation s1, s2, s3, s4, s5, s6, s7, s8, s9;
	MetroStation myPath[SIZE]={'\0'};

	strcpy(red.color, "red");
	strcpy(blue.color, "blue");
	strcpy(green.color, "green");


	strcpy(s1.name, "Haydarpasa"); 		s1.x=0; 	s1.y=0;
	strcpy(s2.name, "Sogutlucesme"); 	s2.x=10; 	s2.y=5;
	strcpy(s3.name, "Goztepe"); 		s3.x=20; 	s3.y=10;
	strcpy(s4.name, "Kozyatagi"); 		s4.x=30; 	s4.y=35;
	strcpy(s5.name, "Bostanci"); 		s5.x=45; 	s5.y=20;
	strcpy(s6.name, "Kartal"); 			s6.x=55; 	s6.y=20;
	strcpy(s7.name, "Samandira"); 		s7.x=60; 	s7.y=40;
	strcpy(s8.name, "Icmeler"); 		s8.x=70; 	s8.y=15;

	//Add several metro stations to the given metro lines.
	addStation(&red, s1); addStation(&red, s2); addStation(&red, s3); addStation(&red, s4); addStation(&red, s5); addStation(&red, s8);

	addStation(&blue, s2); addStation(&blue, s3); addStation(&blue, s4); addStation(&blue, s6); addStation(&blue, s7);

	addStation(&green, s2); addStation(&green, s3); addStation(&green, s5); addStation(&green, s6); addStation(&green, s8);

	// Add red, blue, green metro lines to the Istanbul metro system.
	addLine(&istanbul, red);
	addLine(&istanbul, blue);
	addLine(&istanbul, green);

	// print the content of the red, blue, green metro lines
	printLine(red);
	printLine(blue);
	printLine(green);




	// find the nearest stations to the current and target locations
	MetroStation nearMe = findNearestStation(istanbul, myX, myY);
	MetroStation nearGoal = findNearestStation(istanbul, goalX, goalY);

	printf("\n");

	printf("The best path from %s to %s is:\n", nearMe.name, nearGoal.name);

	// if the nearest current and target stations are the same, then print a message and exit.
	if(equals(nearMe, nearGoal)){
		printf("It is better to walk!\n");
		return 0;
	}

	// Calculate and print the myPath with the minimum distance travelled from start to target stations.
//	findPath(nearMe, nearGoal, myPath);

	if(strlen(myPath[0].name) == 0)
		printf("There is no path on the metro!\n");
	else{
	//	printPath(myPath);
	}


	return 0;

}

