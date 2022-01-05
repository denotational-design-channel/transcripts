## Exploring Denotational Design through the lens of Computer Imagery

**Sean:** And one of those examples would be to look at the way many people think of images which is as two dimensional arrays of pixels and then to consider other representations such as your representation mapping from ℝ² to colors, represented some way. We could do RGB for instance. And also, another representation might be vector graphics which I think is quite superior (already) to two dimensional arrays of pixels, but perhaps not as good as -

**Conal:** I got a little sound effect. What was the second idea?

**Sean:** Oh, just vector graphics

**Conal:** Oh vector graphics, yeah. But vector graphics as a representation?

[**Sean:** I meant denotation and this gets corrected later]

**Sean:** Yeah I guess. I guess what I'm thinking of you have some primitive building blocks like geometric shapes and bezier curves and that kind of thing and graphics constructed that way. I think that's already superior to thinking of things as two dimensional arrays of pixels but perhaps not quite as good as total functions from ℝ² to colors.

**Conal:** Yeah, I mean it's a tiny fraction of what you could express in the general model.

**Sean:** Yes, that's true. That's a good criterion.

**Conal:** There's some interesting things you could look at if you go in that direction of the collection of geometric stuff. On thing is, if you want to do spatial transformation -- that's a pretty common thing you want to do with graphics -- and so if you have a, say, a square and it's represented by this thing that says "here I'm a square at here are my corners", or something like that, or maybe angle and width and things like that, and then you want to apply some spatial transformation to it. How do you do it? And what does it mean to do it correctly? And so what graphics programmers, the way they've been conditioned to think, is to transform the vertices.

**Sean:** That's right. And that's the way I would do it if I was working with some data structure that specified squares as as corners, or sides, or whatever. That's true.

**Conal:** Then that brings the question, is that correct? And that question raises another question which is what does it mean to be correct? And that's the important question. And if you just assume, if I just decide what it means -- that's what people normally do, I just decide what it means. So what are you saying when you decide that's what it means? Do you want this decision to be consistent with anything at all else? Do you want anything to be true about it? Is there something that you think is true if you make this choice and false if you make some other choice? Why not just reverse the vertices, or eliminate them, or multiply them or something like that? Why not all those choices instead?

**Sean:** Oh, you mean in order to implement rotation?

**Conal:** Yeah, exactly. Why don't you just return the empty image?

**Sean:** I see what you're saying. Okay, and you're then led to the question of "what's my underlying model for a square?" and that might lead you in a fruitful direction.

**Conal:** Yeah, and then do that with every single choice you make in programming. Every time I'm about to make a choice [I should ask] so, why do I want this choice. Is there something true about it? Can I just make arbitrary choices about every single thing? Or only the choices that leave me somehow feeling comfortable? And if they leave me feeling uncomfortable I shouldn't make. I think that's probably a big criterion for most programmers , whether they know it or not. And then why not take some completely ludicrous alternative and do that instead. What's better about your alternative? Can you pull anything out of this subjectivity, and make it objective? And I you can't then you're not doing anything like science.

**Sean:** Okay, let me push back for a little bit and say that one could make the argument that geometry in the two dimensional real plane is fairly well understood in a mathematical sense and that there are textbooks out there that talk about what's necessary to rotate an object, or translate it, or scale it.

**Conal:** Okay, so if the people who wrote those textbooks are going to write your program for you then that's somewhat a compelling argument. Maybe a little bit. But you're the one who's going to write the program and you're justifying it by saying that somebody else understands something so how do you know that what you write is compatible with what they understand?

**Sean:** Well I would hope that there would be some theorems around why rotation, let's say the rotation algorithm, is correct.

**Conal:** There could be and those theorems would have something even more important than themselves which is what it means to be correct. If there's some theorem that this is correct then there must be some notation of what "correct" means. And we haven't, so far, said anything that's suggested whether some mathematician's idea of what it would mean to be correct is the same as what we're thinking. You know what I mean? Like there's a "do this and it's correct" and I say "okay, I'll do this and it's correct" but it turns out that his notion of correctness and mine are completely unrelated to each other. Then I've kind of got this false sense of reassurance. So it's really important for me to understand what does he mean by "correct"? And do I want that to be what I mean by correct? And what if I take theorems from two different sources and they have two different notions of correctness and I use both of them. I can't possibly be right, because they disagree with each other, and I agree with both of them so I'm not even agreeing with myself at this point.

**Sean:** Well absolutely, I agree with that statement [if] you take it from two sources, but maybe you don't take it from two sources. So are you gradually leading to suggesting that representing images as functions has this correctness criterion?

**Conal:** First of all I don't _represent_ using functions, those are the _denotations_ not the representations.

**Sean:** Ah, I better be precise with my words here.

**Conal:** If I conceptualize imagary as functions then it's easy for me, without pointing to anyone else for authority to explain _completely_ what I mean for every single operation in my library. I picked a model and then I have a library, a bunch of vocabulary, and now I can define everything in my library _simply_ and _precisely_ in terms of that model. So it's not like me picking it [the model] makes anything true it makes it easy for me to say something that is true. And then we look at it and say "it it at all related to my intuition about imagery. Does it have a useful relationship to my intuition about imagery also"?  If it's something completely unrelated like pairs of [indistingishable TODO: Ask Conal] or it's a sound then we can say "okay that's self consistent but it's really not what I was looking for in an image library". So it should have something to do with my intuition or my vague intent around images and it should be completely well-defined and self consistent _and_ what it means _has to be simple_ and the reason for that is that I'm not very smart. That's the reason for that. And neither are many of my friends. So the simplicity is so we know what we're talking about. The machine-checked or socially checked [side of things] is what keeps me honest, or helps me not make mistakes without noticing them.

**Sean:** I guess what I'm struggling with is that your denotation is functions...

**Conal:** That's mine, but it's not the only possible one.

**Sean:** Right, yes.

**Conal:** I'm not at all arguing for it. I'm saying pick any at all, like the one we're talking about and then say what it means to do spatial transformations. And rotation is one of them. And if you do your thing, what you had in mind for squares it's right. It turns out to be right and you can prove it but if you start trying some other spatial transformations after a while you'll find that it's wrong. The first one you tried, you got lucky in a sense but also you hang out with programmers and that's one of the few that they actually use because it happens to be correct for how they want to implement it. But once you try some other things you'll find out that that implementation choice is actually wrong.

**Sean:** Okay, and can you give me an example of one of the ones that is wrong?

**Conal:** Yeah absolutely. If you take a warp, a non-linear kind of a bend or a twist or something like that. You do that by, you define how you're going to map space -- so a rotation is a function from space to space, [makes hand gestures] something around the origin, that kind of thing. So a warp or a twist or something like that is ... if you take a square and you apply that transformation you won't get a square. You won't get a polygon even because all the interior points if you map them through space they're no longer going to --

**Sean:** I get it now! No, I get it now, because I don't have the vocabulary within that particular, I'm going to call it, denotation to actually draw the square. I just don't have it. Those weird, curved, sides it's going to have probably aren't bezier curves either.

**Conal:** Yeah they're not. Or the first one we try would be bezier and so would the second we try but the third one we try would not be bezier.

**Sean:** Yeah, I'm just suggesting that if I'm only limited to bezier curves there are some warps which will exist which won't map to bezier curves and then I can literally not draw this thing.

**Conal:** Yeah, or what would be more likely to happen is that you would draw it and it would be wrong!

**Sean:** *Laughs*

**Conal:** But you'd be content because you'd say well that's what I defined it to mean. "Look, that's the definition. There it is". But you only get away with that when you don't ask your implementation to be true of anything.

**Sean:** Right, that's funny because I think if it actually was me programming it that's the point where I'd get discontented with the denotation I've chosen. I'd say, "no that actually doesn't apply to my understanding of geometry on the real plane" and then I'd be like "Oh! maybe I should just use the real plane" or something like that.

**Conal:** Yeah, totally. That sounds like a pretty plausible evolution of one's thinking.

**Sean:** Yeah, I just feel like at the point where the square wasn't drawn properly, sorry, the warped square wasn't drawn properly, that's where I'd go "but that's not correct" and then I would realise that, in fact, I do reason about things with more machinery than the denotation I'm actually using. I'd be like "this really wasn't everything. I thought it was everything but there are other things I use to reason about geometry and therefore this is limited and can't possibly be correct and I'm going to need to change my denotation." That was a really great example, Conal, because I did _not_ see it until you mentioned what happens to the sides of the squares in the warp. Okay, that's really cool.

**Conal:** Isn't that funny? And like graphics people, people who are doing graphic programming they're _so_ used to using matrices to represent their spatial transformations that they don't realise they represent almost _no_ spatial transformations.  And all the one they happen to be able to represent, they wouldn't notice this fundamental bug. It works for everything they can represent but that's not because spatial transformations (in general) and polygons like each other, it's because they picked such an incredibly impoverished notion of spatial transformation.

**Sean:** Yeah, that's really interesting. So let me ask you a question back to where we were talking about, say you choose the vector graphics representation as your denotation. I then said "well you could consult mathematical textbooks to see if it was correct or not" and they would have theorems, and so on. What was it about that process that seemed wrong to you? Was it this understanding that actually it wouldn't work for things like warps?

**Conal:** No, it wasn't that, it was the way I interpreted what you said. It may have not been the way you meant it. I interpreted what you said as there are some experts of there who have done a lot of thinking about these kinds of things and it's kind of done, and I get reassurance and I don't need to worry about it anymore. Just knowing that it's out there addresses my concerns.

**Sean:** Oh, I see.

**Conal:** That was how I intepreted what you said.

**Sean:** Right, that wouldn't be very good. No, I guess I did mean actually mean going and studying the actual mathematical textbooks and then hopefully trying to formally verify some theorems in the library. And that might then have led to understanding it was deficient.

**Conal:** Yeah, it might have. It's kind of luck of the draw. It depends on the text you use and how general a notation of spatial transformation they're interested in. And if it's computer graphics then mostly they're going to assume there's nothing out of their favourite representation that they should be interested in, whereas almost everything is outside of it. So in other words they'll have affine and projective kind of things. But also, you don't have to abandon vector graphics at this point. There's another choice and sometimes it's really the right choice. "No darn it, I want my vector graphics!" But I want a nice story and I want to really understand vector graphics. So the technique, the implementation choice of to transform a shape I transform the vertices used to define that shape -- that's the kind of thing that people do. the transform of the shape is the shape of the transform. It's a little homomorphism -- and that equation, that property, _is_ true for some transformations and some shapes, and it's false for others. So instead of abandoning the whole enterprise you can just say, okay, I want to model, I want to understand my transformations as functions on space but I'm not going to allow all transformations. I'm just going to allow some of them. So I can have a restricted subset and there's some property, and hopefully it's a mathematical property, like linearity, something like that, or affineness or projectivity  or something like that, it's kind of a mathematical property, and _then_ now you have that property and now you can say, now you can go back to your question, I want to transform the shape by transforming its control points, and so on, the geometry with that key information, and then you have to ask the question: is that correct or not? And, it completely depends. You really have to consider every shape you're wanting to make and every kind of transformation you're wanting to make and then try to prove that theorem.

**Sean:** Yeah, okay.

**Conal:** And you will _never_ do that unless you think about the specification and you just say "I'm going to implement stuff. I'm a programmer". Then this question will never arise and so you'll get some random hodge-podge of correct and incorrect. Or another possibility is you'll get something right but it's only because you never pushed the edges. Right. It's like I'm going to stay in my little safe zone over here with linear transformations and a few little primitives. Stuff like that. But if you do that maybe you're safe but you missed a whole bunch of interesting stuff you could have done.

**Sean:** That's right, yeah.

**Conal:** If I know what the specification is and I know what the correctness theorems are then I can really go as far as I can while staying within correctness.

**Sean:** Yeah! But the more I think about this particular example, the more I realise that while you're implementing it if you had a keen eye you would notice that there might be deficiencies. Like, a non-linear, or non-affine transformation. You've moved the vertices around. That's perfect. You know you've done that correctly but now you're drawing straight lines between these vertices and saying "well that's what the square looks like". That's the point where you go, this can't possibly be right.

**Conal:** I hope so!

**Sean:** My whole notation of a square that's been transformed that has straight edges is bullshit. That's where you might start thinking more deeply about what you're doing.

**Conal:** Yeah, totally. And there are classes of spatial transformations that have certain properties. Like there's some that are length [or] distance preserving. You take two points, you put them through, and you get two more points. Are they the same distance apart? There's a name for that. Isometric or something like that. And there are ones that preserve angles or don't preserve angles.

**Sean:** Right, so I'll bring us back to our original topic which was that ... I guess I was trying to show a specific example of _denotational design_ to maybe illuminate what the whole thing is about, and I thought maybe I'd look at this example of images, and that when one gets stuck using two dimensional arrays of pixels, when one thinks of images as _being_ that you're hopelessly hampered really in what you can do with those images. Like if you want to zoom in, for instance, everybody knows you can't do that. There's simply not enough information there to do so. You'll just get bigger blocks. So you get blocks of pixels representing what was a pixel before. And rotations would be tricky too.

**Conal:** Yeah, and if you been shackled to a computer for long enough you'll no longer see that as wrong. You'll come to see it as right. "That's what every computer I've ever used has done!"

**Sean:** That's right, yeah.

**Conal:** So there's some other perspective that is independent of the computer programs and the sort of behavior we're using to getting. There's something else. And that other thing is what informs you to say "I don't really like this blockiness". If you didn't have that you would go "oh, blockiness, of course that's always what happens when you zoom in". As if that was your whole universe, you wouldn't even think anything was wrong about it. So I think there's the kind of things we think of as weird artefacts , what I think of as anomalies that we experience when we use software that hasn't been designed well, or, as _you_ said, the data just isn't there. What can I do? There's one artefact or another. Then there's this other thing that say "that's not quite right". It's that other thing that I think we want to pay attention to and make it precise. And that's the _denotation_ for me. That's where that goes.
