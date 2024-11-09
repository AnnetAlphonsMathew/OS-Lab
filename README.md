# OS-Lab
#include <stdio.h>

void main() {
    int n, frame;
    printf("Enter the Length of sequence: ");
    scanf("%d", &n);
    int pg[n];
    
    printf("Enter the Sequence: ");
    for (int i = 0; i < n; i++)
        scanf("%d", &pg[i]);
    
    printf("Enter the number of frames: ");
    scanf("%d", &frame);
    
    int pagefault = 0, hit = 0, k = 0;
    int temp[frame];
    
    printf("\nValues\t");
    for (int i = 1; i <= frame; i++)
        printf("Frame%d\t", i);
    printf("\n");
    
    // Initialize frames to -1
    for (int i = 0; i < frame; i++) {
        temp[i] = -1;
    }
    
    // Process each page
    for (int i = 0; i < n; i++) {
        printf("\n%d =>\t", pg[i]);
        int found = 0;
        
        // Check if page is already in a frame
        for (int j = 0; j < frame; j++) {
            if (temp[j] == pg[i]) {
                found = 1;
                hit++;
                printf("\tHit!!!");
            }
        }
        
        // If page is not in any frame
        if (!found) {
            temp[k] = pg[i];
            k = (k + 1) % frame;
            pagefault++;
            
            // Display current frames
            for (int j = 0; j < frame; j++) {
                if (temp[j] != -1)
                    printf("%d\t", temp[j]);
            }
        }
    }
    
    printf("\nTotal Page Faults: %d\n", pagefault);
    printf("\nTotal Page hits = %d\n", hit);
    printf("Hit ratio = %f", hit / (float)n);
}
