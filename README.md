```c
#include <stdio.h>
#include <string.h>
struct hooman {
    char name[30];
    int energy;
    int loves;
};
struct rawr {
    char name[30];
    int energy;
    int loves;
};
struct hooman hoomans[3] = {
    {"Eca", 30, 40},
    {"Yaya", 80, 20},
    {"Alin", 60, 60}
};
struct rawr rawrs[3] = {
    {"Oyen", 50, 20},
    {"Kiko", 80, 70},
    {"Ewo", 40, 90}
};
struct hooman* namahooman(char* name) {
    for (int i = 0; i < 3; i++) {
        if (strcmp(name, hoomans[i].name) == 0) {
            return &hoomans[i];
        }
    }
    return 0;
}
struct rawr* namarawr(char* name) {
    for (int i = 0; i < 3; i++) {
        if (strcmp(name, rawrs[i].name) == 0) {
            return &rawrs[i];
        }
    }
    return 0;
}
void sifathooman(struct hooman* human) {
    printf("\n%s's energy is %d, and %s's loves is %d.\n", human->name, human->energy, human->name, human->loves);
}
void sifatrawr(struct rawr* meow) {
    printf("\n%s's energy is %d, and %s's loves is %d.\n", meow->name, meow->energy, meow->name, meow->loves);
}
void rubbing(struct hooman* human, struct rawr* meow) {
    printf("\n%s is currently rubbing %s...\n", human->name, meow->name);
    if (meow->loves + 10 > 100) {
        meow->loves = 100;
    } else {
        meow->loves += 10;
    }
    if (human->energy - 5 < 0) {
        human->energy = 0;
    } else {
        human->energy -= 5;
    }   
    printf("%s's energy decreased!\n%s's loves increased!\n", human->name, meow->name);
}
void playing(struct hooman* human, struct rawr* meow) {
    printf("\n%s is currently playing with %s...\n", human->name, meow->name);
    if (meow->energy + 15 > 100) {
        meow->energy = 100;
    } else {
        meow->energy += 15;
    }
    if (human->energy - 10 < 0) {
        human->energy = 0;
    } else {
        human->energy -= 10;
    }   
    printf("%s's energy decreased!\n%s's energy increased!\n", human->name, meow->name);
}
void bubble(struct rawr rawrs[], int n) {
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (rawrs[j].loves < rawrs[j + 1].loves) {
                struct rawr temp = rawrs[j];
                rawrs[j] = rawrs[j + 1];
                rawrs[j + 1] = temp;
            }
        }
    }
}
void urutan() {
    bubble(rawrs, 3);
    printf("\nPets' loves ranking:\n");
    for (int i = 0; i < 3; i++) {
        printf("Pet Name: %s, Loves: %d\n", rawrs[i].name, rawrs[i].loves);
    }
}
int main() {
    int x;
    int start = 1;
    printf("Welcome to Neko Pet Cafe!\n");
    printf("\nThere are three workers and three pets in this pet cafe.\nThe workers are Eca, Yaya, and Alin.\nThe pets are Oyen, Kiko, and Ewo.\n");
    printf("\nThe available commands in this game are:\n");
    printf("1. Rubbing\n");
    printf("2. Playing\n");
    printf("3. Attributes\n");
    printf("4. Pet's Loves Ranking\n");
    printf("5. Exit pet cafe :(\n");
    while (start) {
        printf("\nEnter command (1-5): ");
        if (scanf("%d", &x) != 1) {
            printf ("Command doesn't exist.\n");
            while (getchar() != '\n');
            continue;
        } else if (x == 1) {
            char hoho[30], rara[30];
            printf("\nEnter worker name: ");
            scanf("%s", hoho);
            struct hooman* human = namahooman(hoho);
            if (human == 0) {
                printf("Worker doesn't exist in this cafe.\n");
            }
            else {
                printf("Enter pet name: ");
                scanf("%s", rara);
                struct rawr* meow = namarawr(rara);
                if (meow == 0) {
                    printf("Pet doesn't exist in this cafe.\n");
                } 
                else {
                    rubbing(human, meow);
                }
            }
        } else if (x == 2) {
            char hoho[30], rara[30];
            printf("\nEnter worker name: ");
            scanf("%s", hoho);
            struct hooman* human = namahooman(hoho);
            if (human == 0) {
                printf("Worker doesn't exist in this cafe.\n");
            }
            else {
                printf("Enter pet name: ");
                scanf("%s", rara);
                struct rawr* meow = namarawr(rara);
                if (meow == 0) {
                    printf("Pet doesn't exist in this cafe.\n");
                } 
                else {
                    playing(human, meow);
                }
            }
        } else if (x == 3) {
            char name[30];
            int y;
            printf("\nWhich attribute do you want to check?\n");
            printf("1. Worker\n2. Pet\n");
            printf("Enter command (1-2): ");
            if (scanf("%d", &y) != 1 || (y != 1 && y != 2)) {
                printf("Command doesn't exist.\n");
                while (getchar() != '\n');
                continue;
            } else if (y == 1) {
                printf("\nEnter worker name: ");
                scanf("%s", name);
                struct hooman* human = namahooman(name);
                if (human == 0) {
                    printf("Worker doesn't exist in this cafe.\n");
                } else if (human != 0) {
                    sifathooman(human);
                }
            } else if (y == 2) {
                printf("\nEnter pet name: ");
                scanf("%s", name);
                struct rawr* meow = namarawr(name);
                if (meow == 0) {
                    printf("Pet doesn't exist in this cafe.\n");
                } else if (meow != 0) {
                    sifatrawr(meow);
                }
            }
        } else if (x == 4) {
            urutan();
        } else if (x == 5) {
            start = 0;
        }
    }
    printf("\nThank you for taking care of these cuties!");
    return 0;
}