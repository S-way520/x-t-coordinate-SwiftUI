# x-t-coordinate-SwiftUI
The t-axis is fixed, and the x-axis can adjust the displacement.
# The first part
![IMG_1059](https://github.com/S-way520/x-t-coordinate-SwiftUI/assets/95877651/5fc26077-7502-4eab-8e99-69a33213f218)
# The second part
Code file 1
```swift
import SwiftUI
@main
struct MyApp: App {
    var body: some Scene {
        WindowGroup {
            ContentView()
        }
    }
}
```
Code file 2
```swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        ScrollView([.horizontal, .vertical]) {
            ZStack {
                CustomPathView()
                CoordinateSystemView()
            }
            .frame(width: 400, height: 400)
            .border(Color.blue)
        }
    }
}

struct CustomPathView: View {
    var body: some View {
        ZStack {
            let T0 = 0
            let T1 = 2
            let T2 = 3
            let T3 = 2
            let T4 = 3
            let T5 = 7
            let T6 = 6
            let T7 = 8
            let t0 = 40 * (9 - T0)
            let t1 = 40 * (9 - T1)//280
            let t2 = 40 * (9 - T2)
            let t3 = 40 * (9 - T3)
            let t4 = 40 * (9 - T4)
            let t5 = 40 * (9 - T5)
            let t6 = 40 * (9 - T6)
            let t7 = 40 * (9 - T7)
            Path { path in
                path.move(to: CGPoint(x: 40, y: t0))
                path.addCurve(to: CGPoint(x: 80, y: t1), 
                              control1: CGPoint(x: 50, 
                                                y: t0 + (T1 - T0)), 
                              control2: CGPoint(x: 70, 
                                                y: t1 + (T1 - T0)))
                path.addCurve(to: CGPoint(x: 120, y: t2), 
                              control1: CGPoint(x: 90, 
                                                y: t1 + (T2 - T1)), 
                              control2: CGPoint(x: 110, 
                                                y: t2 + (T2 - T1)))
                path.addCurve(to: CGPoint(x: 160, y: t3), 
                              control1: CGPoint(x: 130, 
                                                y: t2 + (T3 - T2)), 
                              control2: CGPoint(x: 150, 
                                                y: t3 + (T3 - T2)))
                path.addCurve(to: CGPoint(x: 200, y: t4), 
                              control1: CGPoint(x: 170, 
                                                y: t3 + (T4 - T3)), 
                              control2: CGPoint(x: 190, 
                                                y: t4 + (T4 - T3)))
                path.addCurve(to: CGPoint(x: 240, y: t5), 
                              control1: CGPoint(x: 210, 
                                                y: t4 + (T5 - T4)), 
                              control2: CGPoint(x: 230, 
                                                y: t5 + (T5 - T4)))
                path.addCurve(to: CGPoint(x: 280, y: t6), 
                              control1: CGPoint(x: 250, 
                                                y: t5 + (T6 - T5)), 
                              control2: CGPoint(x: 270, 
                                                y: t6 + (T6 - T5)))
                path.addCurve(to: CGPoint(x: 320, y: t7), 
                              control1: CGPoint(x: 290, 
                                                y: t6 + (T7 - T6)), 
                              control2: CGPoint(x: 310, 
                                                y: t7 + (T7 - T6)))
            }
            .stroke(Color.blue, lineWidth: 2)
            
            Circle()
                .frame(width: 10)
                .position(x: 0 * 40 + 40, y: CGFloat(t0))
            Circle()
                .frame(width: 10)
                .position(x: 1 * 40 + 40, y: CGFloat(t1))
            Circle()
                .frame(width: 10)
                .position(x: 2 * 40 + 40, y: CGFloat(t2))
            Circle()
                .frame(width: 10)
                .position(x: 3 * 40 + 40, y: CGFloat(t3))
            Circle()
                .frame(width: 10)
                .position(x: 4 * 40 + 40, y: CGFloat(t4))
            Circle()
                .frame(width: 10)
                .position(x: 5 * 40 + 40, y: CGFloat(t5))
            Circle()
                .frame(width: 10)
                .position(x: 6 * 40 + 40, y: CGFloat(t6))
            Circle()
                .frame(width: 10)
                .position(x: 7 * 40 + 40, y: CGFloat(t7))
        }
    }
}

struct CoordinateSystemView: View {
    var body: some View {
        ZStack {
            // X-Axis
            Path { path in
                path.move(to: CGPoint(x: 40, y: 360))
                path.addLine(to: CGPoint(x: 360, y: 360))
                path.move(to: CGPoint(x: 350, y: 355))
                path.addLine(to: CGPoint(x: 360, y: 360))
                path.addLine(to: CGPoint(x: 350, y: 365))
                // X-axis tick marks
                for i in 1...7 {
                    let x = 40 + CGFloat(i) * 40
                    path.move(to: CGPoint(x: x, y: 360))
                    path.addLine(to: CGPoint(x: x, y: 356))
                }
            }
            .stroke(Color.orange, lineWidth: 1)
            ForEach (1...7, id: \.self) { index in
                Text("\((8 - index) * 1)")
                    .position(x: 20, y: CGFloat(index) * 40 + 40)
                Text("x/m")
                    .position(x: 20, y: 40)
            }
            // T-Axis
            Path { path in
                path.move(to: CGPoint(x: 40, y: 40))
                path.addLine(to: CGPoint(x: 40, y: 360))
                path.move(to: CGPoint(x: 35, y: 50))
                path.addLine(to: CGPoint(x: 40, y: 40))
                path.addLine(to: CGPoint(x: 45, y: 50))
                // T-axis tick marks
                for i in 1...7 {
                    let y = 40 + CGFloat(i) * 40
                    path.move(to: CGPoint(x: 40, y: y))
                    path.addLine(to: CGPoint(x: 44, y: y))
                }
            }
            .stroke(Color.orange, lineWidth: 1)
            ForEach (0...7, id: \.self) { index in
                Text("\(index * 1)")
                    .position(x: CGFloat(index) * 40 + 40, y: 380)
                Text("t/s")
                    .position(x: 360, y: 380)
            }
        }
    }
}

```
