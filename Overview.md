## Acknowledgements
Code sourced from this video: https://youtu.be/kUjHl7zfCeg

# Overview
This makes using lottiefiles easier in swiftui

```swift
import SwiftUI
import Lottie

struct LottiePlusView: UIViewRepresentable{
    let name: String
    let loopMode: LottieLoopMode
    let animationSpeed: CGFloat
    let contentMode: UIView.ContentMode
    @Binding var play: Bool
    
    let animationView: LottieAnimationView
    
    init(name: String, loopMode: LottieLoopMode = .playOnce,
         animationSpeed: CGFloat = 1,
         contentMode: UIView.ContentMode = .scaleAspectFit,
         play: Binding<Bool> = .constant(true)) {
        
        self.name = name
        self.animationView = LottieAnimationView(name: name)
        self.loopMode = loopMode
        self.animationSpeed = animationSpeed
        self.contentMode = contentMode
        self._play = play //Because its a binding bool
    }
    
    func makeUIView(context: Context) -> UIView {
        let view = UIView(frame: .zero)
        view.addSubview(animationView)
        animationView.contentMode = contentMode
        animationView.translatesAutoresizingMaskIntoConstraints = false
        animationView.heightAnchor.constraint(equalTo: view.heightAnchor).isActive = true
        animationView.widthAnchor.constraint(equalTo: view.widthAnchor).isActive = true
        animationView.loopMode = loopMode
        animationView.animationSpeed = animationSpeed
//        animationView.play()
        view.isUserInteractionEnabled = false
        return view
    }
    
    func updateUIView(_ uiView: UIView, context: Context) {
        if play{
            animationView.play { _ in
                play = false
            }
        }
    }
}

```
