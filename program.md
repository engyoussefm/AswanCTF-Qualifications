DECOMPILED FLAG VERIFICATION PROGRAM
-----------------------------------

#include <stdio.h>
#include <stdint.h>

const uint8_t byte_403039[5] = {0xD9,0xB4,0xD1,0xE2,0xDA};
const uint8_t byte_40303E[7] = {0xF9,0x07,0x75,0x85,0x7A,0xB8,0x86};
const uint16_t word_403045[6] = {0x0308,0x01B0,0x03A0,0x01A8,0x01B8,0x0388};

uint8_t __ROR1__(uint8_t value, int shift) {
    return (value >> shift) | (value << (8 - shift));
}

int main() {
    char input[80];
    
    if (fgets(input, sizeof(input), stdin)) {
        // Check 1
        uint8_t v4 = input[14] ^ 0x81;
        int valid = (v4 == 0xED);
        
        if (valid) {
            // Check 2
            for (int i=0; i<5 && valid; i++) {
                v4 ^= input[15+i];
                if (v4 != byte_403039[i]) valid = 0;
            }
            
            // Check 3
            for (int i=0; i<7 && valid; i++) {
                if ((__ROR1__(input[i],2)^0x3F)+20 != byte_40303E[i]) valid=0;
            }
            
            // Check 4
            for (int i=0; i<6 && valid; i++) {
                if (8*(input[7+i]+2) != word_403045[i]) valid=0;
            }
            
            if (valid) printf("You Win!\n");
            else printf("Wrong Flag\n");
        }
    }
    return 0;
}