def main():
    print("Welcome to the Near Misses Finder!")
    n = int(input("Enter the power (2 < n < 12): "))
    k = int(input("Enter the upper limit for x and y (k >= 10): "))
    
    if n <= 2 or n >= 12 or k < 10:
        print("Invalid input. Please make sure n is between 2 and 12, and k is at least 10.")
        sys.exit(1)
    
    smallest_miss = float('inf')
    smallest_miss_values = None
    
    for x in range(10, k + 1):
        for y in range(10, k + 1):
            for z in range(x + 1, k + 1):
                xn_plus_yn = x*n + y*n
                zn = z**n
                zn_plus_1 = (z + 1)**n
                
                if xn_plus_yn > zn and xn_plus_yn < zn_plus_1:
                    miss1 = xn_plus_yn - zn
                    miss2 = zn_plus_1 - xn_plus_yn
                    min_miss = min(miss1, miss2)
                    relative_miss = (min_miss / xn_plus_yn) * 100
                    
                    if min_miss < smallest_miss:
                        smallest_miss = min_miss
                        smallest_miss_values = (x, y, z, int(min_miss), round(relative_miss, 2))
    
    if smallest_miss_values:
        x, y, z, miss, relative_miss = smallest_miss_values
        print("\nSmallest Relative Miss:")
        print(f"x: {x}, y: {y}, z: {z}, Miss: {miss}, Relative Miss (%): {relative_miss}")
    else:
        print("\nNo near misses found.")
    
if _name_ == "_main_":
    main()
