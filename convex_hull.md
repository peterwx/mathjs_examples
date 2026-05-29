This approach plays directly into the strengths of a strict math parser. Instead of stepping through points sequentially, we use pure matrix operations to evaluate the geometry in bulk.
How it works:
- Bulk Edge Detection: For every possible pair of points, we vectorize the cross-product against all other points at the same time. If every other point lies to the right of the directed line $i \to j$, we mathematically know $i \to j$ is an outer boundary edge of the convex hull.
- Filter Hull Points: We filter out any point that is not part of a valid boundary edge.
- Radial Sort: Because brute force returns the hull points unordered, we calculate their geometric center (centroid) and sort them by angle using `atan2`. This automatically connects the dots into a perfectly ordered, counter-clockwise polygon.

```math
# Core Helpers
get_scalar(M, r, c) = sum(subset(M, index(r, c)))
get_count(M) = size(M)[1]

# Vectorized Column Extractors
get_X(pts) = subset(pts, index(range(1, get_count(pts)), 1))
get_Y(pts) = subset(pts, index(range(1, get_count(pts)), 2))

# Vectorized Cross Product (Computes orientation of ALL points relative to directed edge i->j)
cp_vec(pts, i, j) = subtract(multiply(subtract(get_scalar(pts, j, 1), get_scalar(pts, i, 1)), subtract(get_Y(pts), get_scalar(pts, i, 2))), multiply(subtract(get_scalar(pts, j, 2), get_scalar(pts, i, 2)), subtract(get_X(pts), get_scalar(pts, i, 1))))

# Edge Check: Returns 1 if all points lie to the right of (or on) edge i->j, 0 otherwise
is_edge(pts, i, j) = (max(cp_vec(pts, i, j)) <= 0) * (i != j)

# Hull Point Check: Returns 1 if point i is part of ANY valid hull edge, 0 otherwise
is_hull_pt(pts, i) = max(map(range(1, get_count(pts)), anon(j) = is_edge(pts, i, j))) > 0

# Raw Data Preparation
Points_Raw = matrix([[2, 1], [1, 5], [4, 7], [8, 6], [6, 2], [5, 9], [3, 3]])

# 1. Identify Unordered Hull Points
hull_indices = filter(range(1, get_count(Points_Raw)), anon(i) = is_hull_pt(Points_Raw, i))
Unordered_Hull = subset(Points_Raw, index(hull_indices, [1, 2]))

# 2. Radial Sort to Order the Polygon Boundary
cx = mean(get_X(Unordered_Hull))
cy = mean(get_Y(Unordered_Hull))
get_angle(pts, i, cx, cy) = atan2(get_scalar(pts, i, 2) - cy, get_scalar(pts, i, 1) - cx)
angle_comp(pts, cx, cy) = anon(i, j) = get_angle(pts, i, cx, cy) - get_angle(pts, j, cx, cy)
sorted_hull_indices = sort(range(1, get_count(Unordered_Hull)), angle_comp(Unordered_Hull, cx, cy))

# 3. Final Execution
Final_Hull = subset(Unordered_Hull, index(sorted_hull_indices, [1, 2]))
```