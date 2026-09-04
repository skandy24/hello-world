import 'package:flutter/material.dart';

void main() {
  runApp(const BookCommunityApp());
}

class BookCommunityApp extends StatelessWidget {
  const BookCommunityApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      title: 'Book Community',
      theme: ThemeData(
        colorScheme: ColorScheme.fromSeed(
          seedColor: Colors.deepPurple,
        ),
        useMaterial3: true,
      ),
      home: const HomePage(),
    );
  }
}

class HomePage extends StatefulWidget {
  const HomePage({super.key});

  @override
  State<HomePage> createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  int selectedIndex = 0;

  final List<Widget> pages = const [
    HomeTab(),
    SwapTab(),
    ReadingTab(),
    ProfileTab(),
  ];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text(
          'BookCircle 📚',
          style: TextStyle(fontWeight: FontWeight.bold),
        ),
        centerTitle: false,
      ),

      body: pages[selectedIndex],

      bottomNavigationBar: NavigationBar(
        selectedIndex: selectedIndex,
        onDestinationSelected: (index) {
          setState(() {
            selectedIndex = index;
          });
        },
        destinations: const [
          NavigationDestination(
            icon: Icon(Icons.home_outlined),
            selectedIcon: Icon(Icons.home),
            label: 'Home',
          ),
          NavigationDestination(
            icon: Icon(Icons.swap_horiz),
            label: 'Swap',
          ),
          NavigationDestination(
            icon: Icon(Icons.groups_outlined),
            selectedIcon: Icon(Icons.groups),
            label: 'Reading',
          ),
          NavigationDestination(
            icon: Icon(Icons.person_outline),
            selectedIcon: Icon(Icons.person),
            label: 'Profile',
          ),
        ],
      ),
    );
  }
}


// ---------------- HOME ----------------

class HomeTab extends StatelessWidget {
  const HomeTab({super.key});

  @override
  Widget build(BuildContext context) {
    return ListView(
      padding: const EdgeInsets.all(16),
      children: [

        const Text(
          'Welcome, Reader 👋',
          style: TextStyle(
            fontSize: 26,
            fontWeight: FontWeight.bold,
          ),
        ),

        const SizedBox(height: 8),

        const Text(
          'Discover books, swap with others and join reading communities.',
          style: TextStyle(fontSize: 16),
        ),

        const SizedBox(height: 24),

        // Search
        TextField(
          decoration: InputDecoration(
            hintText: 'Search for books...',
            prefixIcon: const Icon(Icons.search),
            border: OutlineInputBorder(
              borderRadius: BorderRadius.circular(15),
            ),
          ),
        ),

        const SizedBox(height: 24),

        const Text(
          'Popular Books',
          style: TextStyle(
            fontSize: 21,
            fontWeight: FontWeight.bold,
          ),
        ),

        const SizedBox(height: 12),

        BookCard(
          title: 'Atomic Habits',
          author: 'James Clear',
          status: 'Available for Swap',
        ),

        BookCard(
          title: 'The Alchemist',
          author: 'Paulo Coelho',
          status: 'Available for Swap',
        ),

        BookCard(
          title: 'Harry Potter',
          author: 'J. K. Rowling',
          status: 'Available for Swap',
        ),
      ],
    );
  }
}


// ---------------- BOOK CARD ----------------

class BookCard extends StatelessWidget {
  final String title;
  final String author;
  final String status;

  const BookCard({
    super.key,
    required this.title,
    required this.author,
    required this.status,
  });

  @override
  Widget build(BuildContext context) {
    return Card(
      margin: const EdgeInsets.only(bottom: 12),
      child: ListTile(
        leading: Container(
          width: 50,
          height: 65,
          decoration: BoxDecoration(
            color: Colors.deepPurple.shade100,
            borderRadius: BorderRadius.circular(8),
          ),
          child: const Icon(
            Icons.menu_book,
            size: 30,
          ),
        ),

        title: Text(
          title,
          style: const TextStyle(
            fontWeight: FontWeight.bold,
          ),
        ),

        subtitle: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Text(author),
            const SizedBox(height: 5),
            Text(
              status,
              style: const TextStyle(
                color: Colors.green,
              ),
            ),
          ],
        ),

        trailing: const Icon(Icons.arrow_forward_ios),
      ),
    );
  }
}


// ---------------- SWAP ----------------

class SwapTab extends StatelessWidget {
  const SwapTab({super.key});

  @override
  Widget build(BuildContext context) {
    return ListView(
      padding: const EdgeInsets.all(16),
      children: [

        const Text(
          'Book Swap 🔄',
          style: TextStyle(
            fontSize: 26,
            fontWeight: FontWeight.bold,
          ),
        ),

        const SizedBox(height: 10),

        const Text(
          'Find people who want to exchange books with you.',
          style: TextStyle(fontSize: 16),
        ),

        const SizedBox(height: 20),

        ElevatedButton.icon(
          onPressed: () {
            ScaffoldMessenger.of(context).showSnackBar(
              const SnackBar(
                content: Text('Add Book feature coming soon!'),
              ),
            );
          },
          icon: const Icon(Icons.add),
          label: const Text('Add My Book'),
        ),

        const SizedBox(height: 20),

        BookCard(
          title: 'Rich Dad Poor Dad',
          author: 'Robert Kiyosaki',
          status: 'Wants to swap',
        ),

        BookCard(
          title: 'Ikigai',
          author: 'Héctor García',
          status: 'Wants to swap',
        ),
      ],
    );
  }
}


// ---------------- READING ----------------

class ReadingTab extends StatelessWidget {
  const ReadingTab({super.key});

  @override
  Widget build(BuildContext context) {
    return ListView(
      padding: const EdgeInsets.all(16),
      children: [

        const Text(
          'Reading Communities 👥',
          style: TextStyle(
            fontSize: 25,
            fontWeight: FontWeight.bold,
          ),
        ),

        const SizedBox(height: 20),

        ReadingEvent(
          title: 'Sunday Book Club',
          book: 'Atomic Habits',
          members: '12 members',
        ),

        ReadingEvent(
          title: 'Mystery Lovers',
          book: 'The Silent Patient',
          members: '8 members',
        ),

        ReadingEvent(
          title: 'Classic Literature',
          book: 'The Great Gatsby',
          members: '15 members',
        ),
      ],
    );
  }
}


// ---------------- READING EVENT ----------------

class ReadingEvent extends StatelessWidget {
  final String title;
  final String book;
  final String members;

  const ReadingEvent({
    super.key,
    required this.title,
    required this.book,
    required this.members,
  });

  @override
  Widget build(BuildContext context) {
    return Card(
      margin: const EdgeInsets.only(bottom: 15),
      child: Padding(
        padding: const EdgeInsets.all(16),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [

            Text(
              title,
              style: const TextStyle(
                fontSize: 19,
                fontWeight: FontWeight.bold,
              ),
            ),

            const SizedBox(height: 8),

            Text('📖 $book'),

            const SizedBox(height: 5),

            Text('👥 $members'),

            const SizedBox(height: 12),

            ElevatedButton(
              onPressed: () {},
              child: const Text('Join Reading Session'),
            ),
          ],
        ),
      ),
    );
  }
}


// ---------------- PROFILE ----------------

class ProfileTab extends StatelessWidget {
  const ProfileTab({super.key});

  @override
  Widget build(BuildContext context) {
    return Center(
      child: Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: [

          const CircleAvatar(
            radius: 50,
            child: Icon(
              Icons.person,
              size: 50,
            ),
          ),

          const SizedBox(height: 15),

          const Text(
            'Book Lover',
            style: TextStyle(
              fontSize: 24,
              fontWeight: FontWeight.bold,
            ),
          ),

          const SizedBox(height: 8),

          const Text('Books swapped: 5'),

          const Text('Reading sessions joined: 8'),

          const SizedBox(height: 20),

          ElevatedButton(
            onPressed: () {},
            child: const Text('Edit Profile'),
          ),
        ],
      ),
    );
  }
}
