// class Solution {
//     public List<List<Integer>> shiftGrid(int[][] grid, int k) {
//         int m = grid.length;
//         int n = grid[0].length;
//         int total = m*n;
//         int big = total*100;
//         List<List<Integer>> res= new ArrayList<>();
//         int[] a = new int[total];

//         for(int i = 0;i<total;i++){
//             a[i] = grid[i/n][i%n];
//         }

//         // for(int i =0;i<total;i++) {
//         //     System.out.print(a[i]+" ");
//         // }

//         for(int i = 0;i<m;i++) {
//             List<Integer> r= new ArrayList<>();
//             for(int j =0;j<n;j++) {
//                 r.add(a[(i*n+j+big - k) % total]);
//             }
//             res.add(r);
//         }

//         return res;
//     }
// }

import java.util.AbstractList;
class Solution {
    public List<List<Integer>> shiftGrid(int[][] grid, int k) {
        final int n = grid.length;
        final int m = grid[0].length;
        final int total = n * m;
        final int shift = k % total;

        return new AbstractList<List<Integer>>() {
            @Override
            public List<Integer> get(int i) {
                return new AbstractList<Integer>() {
                    @Override
                    public Integer get(int j) {
                        int target1D = i * m + j;
                        int source1D = (target1D + total - shift) % total;
                        return grid[source1D / m][source1D % m];
                    }

                    @Override
                    public int size() {
                        return m;
                    }
                };
            }

            @Override
            public int size() {
                return n;
            }
        };
    }
}

// Synced seamlessly with LeetHub Pro
// Pro features: https://bit.ly/leethubpro | Free version: https://bit.ly/leethubv4
// Get it here: https://chromewebstore.google.com/detail/bcilpkkbokcopmabingnndookdogmbna