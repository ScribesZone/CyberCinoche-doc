


# SYSTEM CyberCinoche

    -- CyberCinoche is the software system to be built for the Cinoche company.
    -- The "Cinoche" company is a unique cinema chain with a socially responsible
    -- mission. Rather than maximizing profits, Cinoche aims to foster social
    -- connections by offering "solidarity passes" to disadvantaged groups, such as
    -- isolated students, homeless individuals, migrants, etc. Most viewers pay standard
    -- ticket prices, and the resulting profits are used to subsidize solidarity
    -- pricing.
    -- Cinoche's programming is also distinctive. Instead of screening the latest
    -- blockbuster releases, which are often expensive, its cinemas focus on films
    -- organized around specific themes—such as retrospectives on actors like Brad Pitt
    -- or seasons highlighting lesser-known talent. These themes and film selections are
    -- collaboratively decided by the cinema managers.
    -- While Cinoche operates like a typical cinema chain in many ways, its associative
    -- structure unites independent cinemas with a shared purpose: inclusivity over
    -- profitability. 



# USE CASE MODEL

The use case model describes the system from a functional perspective. It includes actors, subsystems and usecases. Actors are external to the system. They interacts with usecases.
## USE CASE DIAGRAMS 


**UsecaseDiagram**

![diagram](../diagrams/AAAAAAGEs!6HkbHYbDg=.jpeg)


**ImplementationDiagram**

![diagram](../diagrams/AAAAAAGTXWW35h793zE=.jpeg)

## FLOW INFORMATION DIAGRAMS


**PassFlowDiagram**

![diagram](../diagrams/AAAAAAGE!XNWlhkPtM4=.jpeg)


## actor Clerk

```
actor Clerk inherits from Employee
    << internal >>
    usescase ExtendAPass
```


## actor Collaborator

```
actor Collaborator
    << internal >>
```


## actor Controler

```
actor Controler inherits from Employee
    << internal >>
    usescase ControlTickets
```


## actor Employee

```
actor Employee inherits from Collaborator
    << internal >>
```


## actor Manager

```
actor Manager inherits from Collaborator
    << internal >>
    usescase EvaluateASolidarityPass
    usescase ManageMovies
    usescase ManageShowings
```


## actor President

```
actor President inherits from Collaborator
    << internal >>
    usescase BuySomeTickets
    usescase CheckTheProgram
    usescase ManageCinemas
    usescase ManageMovies
    usescase PickupTickets
    usescase SelectMovies
```


## actor Spectator

```
actor Spectator
    << external >>
    usescase BuySomeTickets
    usescase CheckTheProgram
    usescase PickupTickets
```




## system CyberCinoche

```
system CyberCinoche
    subsystem Backoffice
    subsystem Frontoffice

    -- CyberCinoche is the software system to be built for the Cinoche company.
    -- The "Cinoche" company is a unique cinema chain with a socially responsible
    -- mission. Rather than maximizing profits, Cinoche aims to foster social
    -- connections by offering "solidarity passes" to disadvantaged groups, such as
    -- isolated students, homeless individuals, migrants, etc. Most viewers pay standard
    -- ticket prices, and the resulting profits are used to subsidize solidarity
    -- pricing.
    -- Cinoche's programming is also distinctive. Instead of screening the latest
    -- blockbuster releases, which are often expensive, its cinemas focus on films
    -- organized around specific themes—such as retrospectives on actors like Brad Pitt
    -- or seasons highlighting lesser-known talent. These themes and film selections are
    -- collaboratively decided by the cinema managers.
    -- While Cinoche operates like a typical cinema chain in many ways, its associative
    -- structure unites independent cinemas with a shared purpose: inclusivity over
    -- profitability. 
```

## subsystem Backoffice

```
subsystem Backoffice
    system CyberCinoche
    usecase PickupTickets
    usecase ControlTickets
    usecase ExtendAPass
    usecase SellAPass
    usecase SellATicket
    usecase EvaluateASolidarityPass
    usecase ManageShowings
    usecase SelectMovies
    usecase ManageMovies
    usecase ManageCinemas

```

## subsystem Frontoffice

```
subsystem Frontoffice
    system CyberCinoche
    usecase BuySomeTickets
    usecase CheckTheProgram
    usecase RequestAPass

```


## usecase BuySomeTickets
```
usecase BuySomeTickets
    system Frontoffice
    actor President
    actor Spectator

```

## usecase CheckTheProgram
```
usecase CheckTheProgram
    system Frontoffice
    actor President
    actor Spectator

```

## usecase ControlTickets
```
usecase ControlTickets
    system Backoffice
    actor Controler

```

## usecase EvaluateASolidarityPass
```
usecase EvaluateASolidarityPass
    system Backoffice
    actor Manager

```

## usecase ExtendAPass
```
usecase ExtendAPass
    system Backoffice
    actor Clerk

```

## usecase ManageCinemas
```
usecase ManageCinemas
    system Backoffice
    actor President

```

## usecase ManageMovies
```
usecase ManageMovies
    system Backoffice
    actor Manager
    actor President

```

## usecase ManageShowings
```
usecase ManageShowings
    system Backoffice
    actor Manager

```

## usecase PickupTickets
```
usecase PickupTickets
    system Backoffice
    actor President
    actor Spectator

```

## usecase RequestAPass
```
usecase RequestAPass
    system Frontoffice
    actor Spectator

```

## usecase SelectMovies
```
usecase SelectMovies
    system Backoffice
    actor President

```

## usecase SellAPass
```
usecase SellAPass
    system Backoffice

```

## usecase SellATicket
```
usecase SellATicket
    system Backoffice

```




# DOMAIN MODEL


The domain model describes the main concepts of the domain. It includes enumerations, classes and associations.
## DOMAIN DIAGRAM


**DomainDiagram**

![diagram](../diagrams/AAAAAAGE!SzqDEdGNd4=.jpeg)


## enumeration Genre

```
enumeration Genre
    action
    adventure
    biography
    comedy
    crime
    drama
    family
    fantasy
    historical
    horror
    mystery
    sciFi

```

## enumeration Restriction

```
enumeration Restriction
    R
    PG
    PG-13
    TV-MA

```

## enumeration Role

```
enumeration Role
    president
    manager
    employee

```



## class Celebrity
```
class Celebrity
    -- fr=Célébrité
    -- Celebrity in the world of cinema. A celebrity can be either a director, an actor,
    -- both. In the context of CyberCinoche only celebrities that are relevant to past
    -- seasons of future seasons are taken into account. Celebrities do not exist in
    -- isolation. For instance "Angélina Jolie" is recorded as a celebrity because at
    -- some point Angelina' movies were considered as relevant. Selected informations
    -- come from IMDB.
    attributes
        name : String{id}
            -- Firstname and lastname of the celebrity. Sometimes simplified with respect to
            -- IBDM.
        portrait : Image
            -- Portrait from IMDB.
        imdb : URL
        / nbOfActedMovies : Integer
            -- fr=nbDeFilmsJoués
            -- Number of movies acted in (among the small selection of films listed in the
            -- Cinoche framework).
            -- ## Constraints
            -- /nbOfActedMovies = self.actedInMovies->size()
        / nbOfDirectedMovies : Integer
            -- fr=nbDeFilmDirigés
            -- Number of movies directed (among the small selection of films listed in the
            -- Cinoche framework).
            -- ## Constraints
            -- /nbOfDirectedovies = self.directedMovies->size()

    roles
        actedInMovies : Movie[*]
            -- Selection of films in which the celebrity acted as an actor/actress. Only films
            -- deemed relevant by Cinoche are listed. For instance, for Brad Pitt, only a few
            -- selected movies are listed, including past films or movies to be shown in the
            -- future. This contrasts with IBDB, where "all" movies are listed.
        directedMovies : Movie[*]
            -- Selection of movies in which the celebrity acted as the director. Only films
            -- deemed relevant by Cinoche are listed.


```

## class Cinema
```
class Cinema
    -- fr=Cinéma
    -- One of the cinema of the Cincoche consortium.
    attributes
        name : String {id}
        address : String
        city : String
        ticketPrice : Real
        image : Image
        / nbOfScreens : Integer
            -- fr=nbDeSalles
            -- ## Constraints
            -- /nbOfScreens = self.screens->size()
        / nbOfSeats : Integer
            -- fr=nbDePlaces
            -- ## Constraints
            -- /nbOfSeats = self.screens->sum()
        / nbOfAvailableSeats : Integer
            -- fr=nbDePlacesDisponibles
            -- ## Constraints
            -- /nbOfFreeSeats = self.screen->select(state=active).nbOfSeats->sum()
        / nbOfTickets : Integer
            -- ## Constraints
            -- /nbOfTickets = self.screens.nbOfTickets->sum()

    roles
        composite cinoche : Cinoche[1]
        screens : Screen[*]
        manager : Collaborator[1]
        employee : Collaborator[*]
        passes : Pass[*]
            -- All passes created within the context of the given cinema. All passes are listed
            -- regardless of their state. Passes are added but never removed, as they are simply
            -- marked 'expired' when finished.


```

## class Cinoche
```
class Cinoche
    -- Cinoche is an associative structure that brings together independent cinemas. The
    -- unique aspect of Cinoche is that no film is shown upon its initial release.
    -- Instead, cinema managers come together to define a theme and select a number of
    -- films based on a specific theme, such as a season featuring films with Angelina
    -- Jolie or Brad Pitt, or featuring lesser-known actors and actresses.  The list of
    -- movies to be shown is selected in a collaborative way. One of the most notable
    -- features of Cinoche is that this organization provides passes for people with
    -- limited means: unemployed individuals, isolated students, migrants, homeless
    -- individuals, etc. CyberCinoche's mission is to be inclusive rather than
    -- profitable.
    attributes
        name : String {id}
        3DSurcharge : Real
        standardDiscount : Integer
            -- Percentage discount for standard passes.
            -- Currently, this percentage is 10%.
            -- NOTE: This attribute is currently not in use.
        / nbOfCinemas : Integer
            -- ## Constraints
            -- /nbOfCinemas = self.cinemas->size()
        / nbOfScreens : Integer
            -- ## Constraints
            -- /nbOfScreens = self.cinemas.nbOfScreens->sum()
        / nbOfSeats : Integer
            -- ## Constraints
            -- /nbOfSeats = self.cinemas.nbOfSeats->sum()
        / nbOfAvailableSeats : Integer
            -- ## Constraints
            -- /nbOfAvailableSeats = self.cinemas.nbOfAvailableSeats->sum()
        / availabilityRate : Integer
            -- ## Constraints
            -- /availabiltyRate =  self.nbOfAvaiableSeats / nbOfSeats * 100
        / ticketPriceAverage : Real
            -- ## Constraints
            -- /ticketPriceAverage = self.cinema.price->avg()
        / nbOfTickets : Integer
            -- ## Constraints
            -- /nbOfTickets = self.cinemas.nbOfTickets->sum()

    roles
        cinemas : Cinema[*]


```

## class Collaborator
```
class Collaborator
    -- ollaborators are employees of Cinoche cinemas, including one manager for each
    -- location. Additionally, each year a single "president" is elected from among all
    -- collaborators, whether they are managers or not. The president’s role is
    -- primarily to define themes for the upcoming season and to make final decisions in
    -- the movie selection process.
    attributes
        email : Email
        name : String
        role : Role

    roles
        managedCinema : Cinema[0..1]
        employer : Cinema[0..1]


```

## class Movie
```
class Movie
    -- Movies that were suggested during the selection process or movies that are later
    -- scheduled and displayed. The data about movies directly come from IMDB
    -- (https://imdb.com).
    attributes
        title : String {id}
            -- Title of the movie in its original version. The title comes from IMDB.
        state : MovieState
        year : Integer
        poster : Image
            -- Poster of the original version of the movie, as displayed in IMDB.
        summary : String
        description : String
        imdb : URL
        duration : Integer
            -- Duration expressed in minutes. Taken from IMDB.
            -- ## Implementation
            -- AirTable provides a data type for duration. This duration type is used.
        rating : Real
            -- IMDB Rating from 0 (worse) to 10 (best). For instance Logan is ranked at 8.1.
        genre : Genre[1..*]
            -- Genres according to IMDB. Not all genres are consdered.
        restriction : Restriction
            -- Restriction according to IMDB.

    roles
        actors : Celebrity[*]
            -- A selected list of the actors acting in a film. All actors cannot be listed.
            -- Furthermore CyberCinoche's objective is to define themed seasons or seasons based
            -- on selected actors, such as the latest films featuring Angelina Jolie as an
            -- actress or director. Only actors relevant to the given them are be listed.
        director : Celebrity[0..1]
            -- Director of a given movie. To simplify it is assumed that there is at most one
            -- director per movie. In practice for most movies only one is selected based on the
            -- topic of the upcoming season.
        showings : Showing[*]
            -- Showings  of a particular movie in Cinoche' cinemas.


    states MovieState
        suggested
        discarded
        selected
        scheduled
        showing
        ended

```


**MovieStateDiagram**

![diagram](../diagrams/AAAAAAGEsG7F4qfe0Ds=.jpeg)

## class Pass
```
class Pass
    -- A pass (relative to a specific cinema) allows its holder to benefit from
    -- reduced-price tickets in that cinema. For a given showing, a spectator can use
    -- their pass to purchase only one ticket (they cannot invite others with their
    -- pass).
    -- There are two types of pass:
    -- (1) SOLIDARITY PASSES reserved for spectators who apply for them, with supporting
    -- documents. The particularity of these pass is that the discount rate is tailored
    -- to each individual's situation on a case-by-case basis (unemployment, isolated
    -- student, migrants, homeless individuals, etc.). The discount rate can actually go
    -- up to 100%, as CyberCinoche's goal is to foster social connections.
    -- (2) STANDARD PASSES for everyone and providing a 10% discount.
    -- See the PassFlowDiagram.
    -- NOTE: The pass class should actually be divided into several classes separating
    -- the pass request, the pass itself, and possibly related to a Spectator class,
    -- etc. Here, only one class has been specified for the sake of simplification.
    -- Moreover, a single class simplifies the AirTable implementation because AirTable
    -- forms can only create records in one table. Ultimately, the choice to use a
    -- single class is an implementation choice associated with the no-code tool
    -- AirTable.
    attributes
        / number : String {id}
            -- The number of a pass in the form of A83 for instanee where 83 is the pass
            -- identifier.
            -- ## Constraints
            -- 	/number = 'A' + self.id
            -- ## AirTable Implementation
            -- NOTE: The concatenation operator is `&`
        id : Integer
            -- id is an autoincremented number.
            -- ##  AirTable Implementation
            -- Use the AirTable type AutoNumber
        name : String
            -- Firstname and lastname of spectator. This value is compulsary.
        email : Email
            -- Spectator's email. This information is mandatory. It will be used later to
            -- contact the spectator, particularly to notify them following a solidarity
            -- request.
        state : PassState
            -- Pass state. See the PassStateDiagram.
        solidarityRequest : Boolean
            -- Indicate whether the spectator has made a solidarity request or not, for example,
            -- if they are unemployed, an asylum seeker, etc. It is up to the spectator to
            -- determine whether the justifications they provide are likely to qualify for a
            -- solidarity subscription. However, ultimately, it will be a manager who decides.
            -- ## AirTable Implementation
            -- NOTE: Choose a checkbox.
        justifications : String[0..1]
            -- Text used to justify the solidarity pass. This text is filled in, if applicable,
            -- by the spectator. This attribute is mandatory for solidarity passes. It is
            -- undefined for standard passes.
        supportingDocuments : Attachement[*]
            -- Supporting documents attached to a solidarity pass. These documents will be
            -- reviewed by a manager to determine the discount to be granted. 
        discount : Integer[0..1]
            -- Percentage Discount. The discount is automatically set at 10% for standard pass.
            -- When reviewing a subscription request, a manager can set the discount rate they
            -- deem most appropriate based on the spectator situation, with a minimum discount
            -- of 10%. This attribute is only filled in once the request has been reviewed,
            -- hence its optional nature.
            -- ## AirTable Implementation
            -- The 'percent' type should be used in AirTable. However, this AirTable type stores
            -- the percentage as a decimal, for instance 0.75 is displayed as 75%. So take care
            -- of this aspect when writing formulaes. For instance use the formula
            -- "(1-discount)" instead of "(100-discount)".
        start : Date
            -- Start date of the pass. It corresponds to the date of form submission.
            -- ## AirTable Implementation
            -- Use the "Created time" type.
        / end : Date
            -- Date when the pass ends, 1 year after the start date.
            -- ## Constraints
            -- 	/end = self.start + 365    -- pseudo code
            -- ## AirTable Implementation
            -- Use the formula `DATEADD({start},1,'year')`

    roles
        tickets : Ticket[*]
            -- Tickets purchased with the discount associated with this pass.
            -- It is only possible to purchase one ticket per session with a given pass : a
            -- spectator cannot "invite" his or her friends.
        composite cinema : Cinema[1]
            -- Cinema where the pass is valid. While spectators can visit other cinemas, they
            -- will need to pay the full price for those tickets. The pass is only valid at the
            -- cinema where it was purchased.


    states PassState
        toBeEvaluated
        valid
        expired

```


**PassStateDiagram**

![diagram](../diagrams/AAAAAAGE7GCFomTrDXk=.jpeg)

## class Screen
```
class Screen
    -- Cinémas can have any screens, that is rooms where the movies are shown. Because
    -- of the solidarity nature of Cinoche, Cinoche cinemas are usually equiped with
    -- simple yet functionals screens.
    attributes
        / name : String {id}
            -- ## Constraints
            -- /name = self.cinema.name + "-" + self.number
        number : String
        state : ScreenState
        nbOfSeats : Integer
        / cinemaImage : Image
            -- fr=Salle
            -- ## Constraints
            -- /cinemaImage = self.cinema.image
        / ticketPrice : Real
            -- ## Contraints
            -- /ticketPrice = self.cinema.ticketPrice
        / nbOfTickets : Integer
            -- ## Constraints
            -- /nbOfTickets = self.showings.nbOfTickets->sum()

    roles
        showings : Showing[*]
        composite cinema : Cinema[1]


    states ScreenState
        active
        outOfOrder
        closed

```


**ScreenStateDiagram**

![diagram](../diagrams/AAAAAAGEr%2BuJs92Ta2w=.jpeg)

## class Showing
```
class Showing
    -- fr=séance
    -- Session during which a given movie is screened in a theater.
    attributes
        / title : String {id}
            -- The name of the showing composed of the screen following by the movie name and
            -- the schedule.
            -- ## Constraints
            -- /title = self.screen.name + " " + self.movie.name + " " + schedule
        schedule : DateTime
            -- Start of the session as displayed to the spectators on the application, web site
            -- or inforlmation board. 
        state : ShowingState
        / poster : Image
            -- ## Constraints
            -- /poster = self.movie.poster
        / nbOfSeatsInTheScreen : Integer
            -- ## Constraints
            -- /nbOfSeatsInTheScreen = self.screen.nbOfSeats
        / nbOfAvailableSeats : Integer
            -- ## Constraints
            -- /nbOfAvailableSeats = self.nbOfSeatsInTheScreen - self.nbOfTickets
        / ticketPrice : Real
            -- ## Constraints
            -- /ticketPrice = self.screen.ticketPrice
        / nbOfTickets : Integer
            -- ## Constraints
            -- /nbOfTickets = self.tickets-size()

    roles
        composite screen : Screen[1]
        tickets : Ticket[*]
        movie : Movie[1]


    states ShowingState
        movable
        canceled
        scheduled
        ofTheWeek
        ofTheDay
        inProgress
        over

```


**ShowingStateDiagram**

![diagram](../diagrams/AAAAAAGEsJoS3mBpIO8=.jpeg)

## class Ticket
```
class Ticket
    -- Tickets allow a single spectator entry to a screening room to watch a movie.  Due
    -- to Cinoche's community-focused mission, tickets are available at very low prices
    -- and may even be free for select audiences. However tickets are non-refundable
    -- under any circumstances.
    attributes
        / number : String {id}
            -- ## Constraints
            -- -- A pass ticket has this format :  A34.8
            -- -- A regular ticket has this format : X234
            -- /number = 
            -- IF self.pass.notEmpty()
            -- THEN self.pass + '.' + self.id 
            -- ELSE 'X' + self.id  ENDIF
        id : Integer
            -- An autonumberd id : tickets are numbered 1, 2, 3, etc. Each time a new ticket is
            -- created the id is incremented.
            -- ## Implementation
            -- Use the "autonumber" data typ in AirTable.
        state : TicketState
        / fullPrice : Real
            -- ## constraints
            -- /fullPrice = self.showing.ticketPrice
        / discountRate : Integer
            -- ## Constraints
            -- /discountRate = self.pass.discount -- can be undefined
        / price : Real
            -- ## Constraints
            -- /price  = self.fullPrice - (100-self.dicountRate) 
            -- -- Percentages are stored as a coefficient < 1 in AirTable.
            -- -- Therefore, 100 should be replaced with 1.

    roles
        composite showing : Showing[1]
        pass : Pass[0..1]
            -- A ticket may have been purchased with or without a pass. 


    states TicketState
        purchased
        controled
        unused

```


**TicketStateDiagram**

![diagram](../diagrams/AAAAAAGE91PRb1G%2BrFs=.jpeg)





# IMPLEMENTATION MODEL


**ManageCinemasInterfaceDiagram**

![diagram](../diagrams/AAAAAAGE8lXSfzmXuUI=.jpeg)

